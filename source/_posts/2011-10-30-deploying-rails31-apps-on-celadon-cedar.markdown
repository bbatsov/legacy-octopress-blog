---
layout: post
title: "Deploying Rails 3.1 applications on Heroku's Celadon Cedar
stack"
comments: true
categories:
- Ruby
- Ruby on Rails
- Heroku
---

## Prelude

[Heroku](http://heroku.com) is an amazing cloud hosting solution. It's extremely well
documented, very easy to start with, very stable and provides you with
the option to use free hosting for some small applications.

While Heroku is generally known as a Ruby on Rails hosting company,
since their acquisition by SalesForce last year, they've expanded
their deployment options a lot. Currently Ruby, Java, Scala, Clojure,
Python and Node.js are all officially supported (on the Cedar Celadon
stack) and more will probably come very soon.

All of our company's applications are using
[Ruby on Rails 3.1.x](http://guides.rubyonrails.org/) and are
targeting the [MRI 1.9.2](http://ruby-lang.org). Those two facts are
the reason that we're using Heroku's
[Celadon Cedar](http://devcenter.heroku.com/articles/cedar) deployment
stack. Celadon Cedar is currently in beta, but it offer a lot of
benefit over the old (stable) Bamboo stack (which also support Rails
3.1 apps and Ruby 1.9.2). For instance - Celadon is aware of the Rails
3.1 asset pipeline and can compile the assets automatically when you
deploy your apps to Heroku. With Bamboo you have to precompile the
resources, which is a very tedious task.

While our experience with Heroku has been very positive in
general, we've hit some bumps along the road, so I've decided to share
some of the problems and their solutions with everyone.

<!--more-->

## Background

There are some things to keep in mind before deploying to Heroku:

* You can't upload files to Heroku. This means that if you're using a
gem such as [CarrierWave](https://github.com/jnicklas/carrierwave) (or
[PaperClip](https://github.com/thoughtbot/paperclip)) for file uploads
it should be configured to use some cloud storage (e.g. Amazon
S3). There is only one writeable folder on Heroku and this is the
**tmp** folder that you should configure as a tmp folder for your
uploads as well.

* Your app should run on Ruby 1.9.2 (the Celadon
Cedar stack, doesn't support Ruby 1.8.x).

* Your `rake assets:precompile` task should (ideally) not invoke any database related
operations.

* You should use PostgreSQL as your local development database to
avoid potential differences between the production and the development
database.

* You should add the `heroku` gem to your `Gemfile`.

* You should install the `taps` gem if you'd like to use `heroku
db:pull` or `heroku db:push`.

## Preparations

#### Configure CarrierWave to use cloud storage

Here's a sample **carrierwave.rb**, that you can put in **config/initializers/** folder:

``` ruby config/initializers/carrierwave.rb
if Rails.env.test? # Store the files locally for test environment
  CarrierWave.configure do |config|
    config.storage = :file
    config.enable_processing = false
  end
end

if Rails.env.development? or Rails.env.production? # Using Amazon S3 for Development and Production
  CarrierWave.configure do |config|
    config.root = Rails.root.join('tmp')
    config.cache_dir = 'uploads'

    config.storage = :fog
    config.fog_credentials = {
        :provider => 'AWS', # required
        :aws_access_key_id => 'key_id', # required
        :aws_secret_access_key => 'access_key', # required
    }
    config.fog_directory = 'empoweronrails' # required
  end
end
```

#### Disable db access during rake assets:precompile

Some gems (like Rails Admin) access the database during the
initialization of the app. The app initialization is ran by default
when you invoke:

`rake assets:precompile`

This is not a problem on your development machine, but it's
problematic on Heroku, since the regular database.yml is discarded
there. Add this:

`config.assets.initialize_on_precompile = false`

somewhere near the end of your **application.rb** file and it will
suppress the initialization on precompile.

#### Enable assets compilation

It's absolutely required to have this line:

`config.assets.compile = true`

in your **production.rb** file if you want your assets to be compiled
automatically by Heroku (which I highly recommend).

#### Use thin or unicorn as the application server

By default, your app's web process runs `rails server`, which uses
Webrick. This is fine for testing, but for production apps you`ll want
to switch to a more robust webserver. I personally use Thin
(recommended by Heroku). Add this to your Gemfile:

`gem 'thin'`

and this to your Procfile (create it if it doesn't already exist):

`web: bundle exec rails server thin -p $PORT`

The creation of the Procfile is very important! You can use the
[foreman](https://github.com/ddollar/foreman) gem to test the
correctness of the Procfile locally.

Alternatively you can use unicorn. While I haven't used Cedar with
Heroku yet, I've read some nice articles, like this
[one](http://michaelvanrooijen.com/articles/2011/06/01-more-concurrency-on-a-single-heroku-dyno-with-the-new-celadon-cedar-stack/),
according to which one can gain significant performance boost with
unicorn.

#### Optimize your slug's size

Your slug size is displayed at the end of a successful compile. You
can roughly estimate slug size locally by doing a fresh checkout of
your app, deleting the `.git` directory, and running `du -hsc`.

Smaller slugs can be transferred across the dyno grid more quickly,
allowing for a faster spin-up speed on your dynos. Generally speaking,
any slug under 15MB is small and nimble; 30MB is average; and 40MB or
above is weighty. If you find your app getting into the 40MB+ range,
you may want to look into some techniques (such as removing unneeded
dependencies or excluding files via `.slugignore`) to reduce the size.

If your repository contains files not necessary to run your app, you
may wish to add these to a `.slugignore` file in the root of your
repository.

## Deployment

First you should create a Heroku application on the Cedar Celadon stack.

`heroku create --stack cedar`

This step will automatically add a git remote called **heroku** to
your git repo's config. Afterwards the deployment is as simple as
pushing a branch (e.g. **master**) to this remote:

`git push heroku master`

Keep in mind that one Heroku app corresponds to exactly one git
branch. We keep a **production** branch for production deployments and
a **master** branch for development deployments.

The last step is to initialize your database. You have two options -
you can either load the db schema or push an existing database:

`heroku run rake db:schema:load`

or

`heroku db:push`

`db:push` takes as an optional parameter the URL of the db to push to
heroku in the following format
`db://username:password@host/dbname`. For example the url for a local
SomeApp db is probably
`postgres://someapp:someapp@localhost/someapp`. If you
don't supply the URL it will be automatically conjured by inspecting
the **database.yml** file of the project you were in, while issuing the
command.

## Troubleshooting

If you're lucky your deployment will go without a hitch and you
won't have to ever read this section of the manual. Most people won't
be so lucky. :-)

#### Errors during deployment

If you get an error during the deployment process the cause of the
problem will be in front of your eyes. Never-the-less here are some of
the most common problems:

* missing Gemfile.lock
* Gemfile.lock that doesn't match the project's Gemfile (this happens if you have OS specific gems in your Gemfile)
* db access on `assets:precompile`
* you forgot the run all specs and cucumber scenarios before
  deployment ;-)

#### Other errors

Obviously you need to take a look at the stack trace to gain some
insight about the nature of the problem. You can do this very easy:

`heroku logs`

Some of the most common errors you'll encounter:

* you forgot to run some migration(s)
* you forgot to turn on asset compilation
* you forgot to run all specs and cucumber scenarios before the deployment

## Misc

#### Dealing with the database on Heroku

You can easily apply migrations to the production database. Just run:

`heroku run rake db:migrate`

If you want to retrieve the production database locally use the following command:

`heroku db:pull postgres://username:password@localhost/dbname`

If you want to push your local db to production run the following command:

`heroku db:push`

Be very careful about the last command! **It will wipe out and replace the current production database!**

#### Running a console

Running the Rails console on Heroku is astonishingly easy. Just run:

`heroku run rails console`

## Epilogue

Heroku and Rails are moving targets, which causes a bit of a headache
from time to time. Hopefully this short article will save some of you
some of that headache.

