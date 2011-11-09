---
layout: post
title: "Django 1.3 vs Rails 3: A not so final showdown"
categories:
- Ruby
- Rails
- Python
- Django
---

## Prelude

I've recently started a new job at an American start-up company. My
position in the company is the one of Technical Lead - the person responsible for
the selection of technologies around which the projects are being
built. Since we'll be doing mostly web development we've had a long
kick-off discussion with the company's CTO about the direction which we should
initially take. He had PHP in mind, but I convinced him that Ruby or
Python would make much better platforms for our futures apps. So he
tasked me to research the two leading frameworks in the Ruby and
Python land - namely Ruby on Rails 3 and Django 1.3. I had a week to
prepare some prototypes with both and create on overview for my
boss. I had some experience with Rails 2 a few years back and I have
fairly decent knowledge of Ruby. My Python is not as fluent
(admittedly), but still - I've played a lot with Python
recently. Django, however, was completely new to me. In this article
I'll try to compare the frameworks in a totally friendly way; if
you've expected an epic flame war post you may very well stop reading
here. I'm obviously no Rails/Django guru, so if I've
written something that is wrong - please feel free to correct me.

Please, keep in mind that a short comparison article cannot even begin
to scratch the immense power and complexity of such frameworks. The overview,
that you'll find here is a bit on the superficial side, but it should
give you enough pointers to get you started.

Hopefully this article will be useful to people that are in the same
boat as was - picking between Rails and Django.

## Setup & Getting started

### Rails

#### Linux & OSX

The recommended (by me) way to install Ruby and Ruby on Rails 3.x is via
[RVM](https://rvm.beginrescueend.com/). RVM allows you to have several
version of Ruby installed at the same time and to easily switch
between them. It also allows you to create gem sets, which are quite
handy in testing. After you've installed RVM it's easy to install any
Ruby interpreter and Rails. This example shows how to get RVM, MRI 1.9.2
and Rails current (3.0.9):

``` bash
$ bash < <(curl -s https://rvm.beginrescueend.com/install/rvm)
$ echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" # Load RVM function' >> ~/.bash_profile
$ source ~/.bash_profile
$ rvm install 1.9.2
$ rvm use 1.9.2 --default
$ which ruby
~/.rvm/rubies/ruby-1.9.2-p180/bin/ruby
$ ruby -v
ruby 1.9.2p180 (2011-02-18 revision 30909) [i686-linux]
$ gem install rails
$ rails -v
Rails 3.0.9
```

Since RVM builds Ruby environments from source you might need to
install a few dependencies first. After you've install RVM it will
output those packages as instructions.

If you're using Z Shell (like me) you should replace .bash_profile
with .zshenv or .zshrc.

#### Windows

While there are many ways to get Ruby on Rails installed on a Windows
host, the simplest is certainly to use the [RailsInstaller](http://railsinstaller.org/). It has only one
little drawback - currently it comes with Ruby 1.8.7 bundled, but the
recent beta already features Ruby 1.9.2.

#### Your first Rails app

``` bash
$ rails new railsdemo
      create
      create  README
      create  Rakefile
      create  config.ru
      create  .gitignore
      create  Gemfile
      create  app
      create  app/controllers/application_controller.rb
      create  app/helpers/application_helper.rb
      create  app/mailers
      create  app/models
      create  app/views/layouts/application.html.erb
      create  config
      create  config/routes.rb
      create  config/application.rb
      create  config/environment.rb
      create  config/environments
      create  config/environments/development.rb
      create  config/environments/production.rb
      create  config/environments/test.rb
      create  config/initializers
      create  config/initializers/backtrace_silencers.rb
      create  config/initializers/inflections.rb
      create  config/initializers/mime_types.rb
      create  config/initializers/secret_token.rb
      create  config/initializers/session_store.rb
      create  config/locales
      create  config/locales/en.yml
      create  config/boot.rb
      create  config/database.yml
      create  db
      create  db/seeds.rb
      create  doc
      create  doc/README_FOR_APP
      create  lib
      create  lib/tasks
      create  lib/tasks/.gitkeep
      create  log
      create  log/server.log
      create  log/production.log
      create  log/development.log
      create  log/test.log
      create  public
      create  public/404.html
      create  public/422.html
      create  public/500.html
      create  public/favicon.ico
      create  public/index.html
      create  public/robots.txt
      create  public/images
      create  public/images/rails.png
      create  public/stylesheets
      create  public/stylesheets/.gitkeep
      create  public/javascripts
      create  public/javascripts/application.js
      create  public/javascripts/controls.js
      create  public/javascripts/dragdrop.js
      create  public/javascripts/effects.js
      create  public/javascripts/prototype.js
      create  public/javascripts/rails.js
      create  script
      create  script/rails
      create  test
      create  test/fixtures
      create  test/functional
      create  test/integration
      create  test/performance/browsing_test.rb
      create  test/test_helper.rb
      create  test/unit
      create  tmp
      create  tmp/sessions
      create  tmp/sockets
      create  tmp/cache
      create  tmp/pids
      create  vendor/plugins
      create  vendor/plugins/.gitkeep
$ rails s
```

As you can see the structure of a Rails project consists of quite a
few folders and files. This is a bit intimidating at first, but
becomes quite valuable once you've used to the predefined
structure. You'll find a good overview of the structure [here](http://ruby.railstutorial.org/book/ruby-on-rails-tutorial#sec:the_first_application).

Open your browser and type
[http://localhost:3000](http://localhost:3000) as the url. If
everything is OK you'll see a Rails welcome page.

At this point you should probably either start playing with
scaffolding or read the rest of this article and start playing with
scaffolding afterwards :-) For instance you can try:

``` bash
$ rails g scaffold User first_name:string last_name:string email:string password:string
$ rake db:migrate
$ rails s
```

Open your browser and type
[http://localhost:3000](http://localhost/users:3000) as the
url. "Magic" like this made Rails famous originally.

By default Rails apps use SQLite as a database backend, so might have
to install it as well.

The rails script is useful for various tasks - code generation,
plug-in installation, running a rails console, running a development
web server, etc.

## Django

#### Linux

I prefer to install django from the distribution's package manager. On
a Red Hat distro like Fedora I would do:

``` bash
$ sudo yum install Django
```

And on a Debian system:

``` bash
$ sudo apt-get install python-django
```

A popular alternative (that would work for OSX and Windows users as
well) to this distro-specific approach is to use a
python package manager like [easy_install](http://packages.python.org/distribute/easy_install.html) or [pip](http://pypi.python.org/pypi/pip).

#### Windows

The [Bitnami Django stack](http://bitnami.org/stack/djangostack) is the simplest way to get Django and
everything that it requires in a single step.

#### Your first app

``` bash
$ django-admin startproject djangodemo
$ ll djangodemo
total 16
-rw-r--r-- 1 bozhidar bozhidar    0 Jun 19 09:45 __init__.py
-rwxr-xr-x 1 bozhidar bozhidar  503 Jun 19 09:45 manage.py*
-rw-r--r-- 1 bozhidar bozhidar 5039 Jun 19 09:45 settings.py
-rw-r--r-- 1 bozhidar bozhidar  577 Jun 19 09:45 urls.py
$ cd djangodemo
$ ./manage.py runserver
```

Compared to Rails, Django created a much simpler project
structure. There are only four files in here and only two are actual
Django configuration files - settings.py and urls.py. manage.py is
just a script useful for managing some aspects of the project (similar
to the rails script) - it can sync the model with the database, run a
development web server, run a django console, etc.

To test the new project open
[http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your browser.

## Features at a glance

### Rails

#### Convention over configuration

The centerpiece of Rails's philosophy is called convention over
configuration(CoC). This basically means that a Rails project has a
predefined layout and sensible defaults. All components (models,
views, controllers, layouts, css, javascript, etc) have standard
places where you should drop them and the application picks them up without
any additional effort on your part.

People seem to underestimate the importance of CoC in practice
initially - it
makes it a lot easier to reason about a project and a lot easier to
configure the project. On the other hand if some of the defaults don't
work for you - you'd have to jump through some hoops. Recent versions
of Rails, however, have made it a lot easier to tweak the defaults.

All in all I feel that CoC is a big win for developers and I guess
many people share my opinion since CoC can now be found in many other
frameworks as well.

#### MVC to the bone

Rails is a classical Model-View-Controller full stack web framework -
it handle all aspects of a typical web application. What separates it
from most of the MVC frameworks around is the heavy emphasis on
[REST](http://en.wikipedia.org/wiki/Representational_State_Transfer). The
domain objects are treated as resources and could be handled in a
uniform manner using just the standard HTTP verbs like GET, PUT,
DELETE, POST. REST is extremely good fit for data driven applications.

As usual the model houses the application's business logic, the
controller invokes functionality from the model layer and feeds the
resulting data to the view layer, which display the data in a
meaningful way to the user.

The model layer is the home of your domain objects and the business
logic surrounding them. Domain objects (a.k.a. entities) are mapped to
database tables (at least in RDBMS). Unlike most object relational
mappers Rails's ActiveRecord (the default ORM; could be substituted
with something else if you wish) doesn't require you to explicitly
declare the structure of the objects, but rather extracts it
automatically from your DB table definitions. A simple class, modeling
an application user might look like this:

``` bash
class User < ActiveRecord::Base
  validates :first_name, :last_name, :email, :password, :presence => true
  validates :password, confirmation: true
end
```

Note that the validation methods are entirely optional (but highly
recommended) - the class could have very well had an empty body. Rails
would know to look for a table named Users in the database and extract
the field information from it.

Rails generates automatically for us "finders" that we can use to make
queries about objects in pure Ruby. It also provides an elegant DSL to
express relationships between various model classes (belongs_to,
has_many, etc)

In the view layer Rails has traditionally relied on HTML templates
with Ruby code embedded in them (html.erb). There are a lot of
community contributed alternatives, however, with HAML being the most
prominent one. On a similar note Rails allows you to use SASS as a
replacement for traditional CSS.

Another centerpiece in Rails is the "Don't Repeat Yourself"(DRY)
principle. In the view layer partial templates, layouts and helpers
are some of the tools available to help you abide by that
principle. You'll certainly make heavy use of them in your
applications so you should pay them some special attention.

#### Database migrations

Everyone that has done some serious programming knows that it's not
realistic to presume that the initial database schema won't ever
change - fields get added/removed, new tables get introduced,
etc. All those changes are commonly referred to as "migrations" and
traditionally every team unrolls its own handling of the problem. On
my last job I was tasked at some point to write a tool in Java that
analyzed a config file and a directory structure filled with SQL
scripts and applied them selectively to various target databases. In
Rails you get this functionally for free - you can express your
migrations as simple Ruby scripts and you can use rake to generate the
appropriate SQL statements for any supported database. Here's a simple
migration script, that creates the Users table:

``` ruby
class CreateUsers < ActiveRecord::Migration
  def self.up
    create_table :users do |t|
      t.string :first_name
      t.string :last_name
      t.string :email
      t.string :password

      t.timestamps
    end
  end

  def self.down
    drop_table :users
  end
end
```

The up method gets invoked when the migration is applied and the down
method gets invoked when it's reverted. Rails 3.1 will offer even more
elegant migrations. To execute all migrations:

``` bash
$ rake db:migrate
```

#### Ajax from within

Rails features tight integration with JavaScript and AJAX. Versions
prior to 3.1 shipped by default the prototype and scriptaculous
JavaScript libraries. In
version 3.1 jQuery will replace them as the default JavaScript
library.

Making and handling AJAX requests in Rails is generally very easy - a
big advantage in today world ruled by rich and dynamic web UIs.

#### Extensibility

Rails is extendable through a multitude of community supplied plugins
that could add incredible functionality to your apps for free. Some of
my favorite plugins are [jQuery for Rails](https://github.com/indirect/jquery-rails),
[client side validations](https://github.com/bcardarella/client_side_validations) and [Rails Admin](https://github.com/sferik/rails_admin).

#### Testing is not optional

What I particularly like about Rails is that it heavily promotes
testing your code. All of the Rails generators would generate test
stubs, that you'll do good to fill in. Rails supports all major Ruby test
frameworks - Test::Unit, RSpec, Cucumber. You have fixtures support, test
database support, the ability to run unit and functional test
separately. I don't recall using any other framework that pays as much
attention to having tests as Rails and for that I can only
congratulate the Rails team.

#### Compatibility with Ruby versions

There are two major version of Ruby out there presently - Ruby 1.8.7
and Ruby 1.9.2. Ruby 1.9.2 offers substantial language and performance
improvements, so you should be pleased to hear that Rails supports
both major Ruby versions. Rails 4.0 will drop support for Ruby 1.8.x.

Rails can also be run on top of JRuby and Rubinius.

#### Deployment options

The most common deployment options for Rails are currently Apache
HTTPD or NginX and Phusion Passenger (mod_rails). People shopping for
cloud Rails deployment should definitely take a look at Heroku.

Rails also runs on alternative Ruby implementations like JRuby and
Rubinius (as mentioned above), that offer exciting new possibilities. For instance using
JRuby allows you to deploy a Rails app into a Java application server
like JBoss or Glassfish and to tap into all those great Java libraries
and frameworks around. Using JRuby also gives you the opportunity to
deploy your apps on Google's App Engine.

### Django

#### A simpler project layout

While I had some experience with Rails from a couple of years ago,
Django was something totally new to me. I expected it to be more or
less Rails for Python, but when I created my first Django app I was
surprised to see that the project folder consisted of only three
files (I'm obviously not counting the python package file
__init__.py).

My initial surprise aside it turned out that most differences were
just superficial and that Django and Rails have quite a lot of
similarities. I'll, however, speak a bit more about the different
stuff than the similar stuff.

#### MVC(MTV), Django style

While Django is a MVC controller framework as well, it's built around a
different mindset. Django is totally configurable and minimalistic
framework that empowers the developers to tailor it to their needs.

A Django project is comprised of autonomous and reusable apps. Apps on
the other hand are comprised of models, views and templates. Django
differs a bit in terminology with Rails - the Rails controllers are
views in Django and the Rails views are called templates in Django. You
can sometimes hear that Django is a Model-Template-View framework -
that shouldn't confuse you. Although the terminology is different the
principles are the same.

Django's default ORM is somewhat reminiscent of frameworks like
Hibernate. Entity classes declare explicitly the all the
attributes. Let's consider again the User model class:

``` python
from django.db import models

class User(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
    email = models.EmailField()
    password = models.CharField(max_length=30)
```

Both approaches have their strengths and weaknesses an usual. In
Django's case we have increased verbosity, but on the other had we
don't have to inquire the database to figure out the exact definition
of model records.

Like in Rails we get useful "finders" that can be used to query for model
objects in pure python (as opposed to using sql).

#### In the template layer

While ERB is basically HTML with Ruby embedded in it, Django features
a custom templating language with it's own (extendable) tag
library. This generally means that Django templates tend to be a bit
cleaner than Rails's templates, since you're not allowed to abuse them
very much. On the other hand you can do virtually anything by
embedding code directly in a template, so as usual - each design
decision has its pros and cons.

Django supports alternative templating libraries, so you're covered in
case you don't like the default one.

Django also features a powerful form generation/handling facilities
that integrate seamlessly with the templating layer. For instance - it
very easy to generate a form matching the structure of a domain model
object with automatic property validation.

#### You're in charge

Django has doesn't adhere to the Rails CoC philosophy. It's assumed
that developers know best what layout and configurations options make
the most sense in their applications. I haven't played that much with
Django yet, but I still haven't come by two different Django apps that
are structured in the same manner. While I understand the benefits of
Django's approach I still prefer Rails's approach. I've worked long
enough to know that you're rarely in the position to make better
decisions about the structure and the defaults of your app, than the
exceptional developers with huge experience that develop frameworks
like Rails and Django.

To illustrate this consider the strong emphasis Rails places on
REST. In Django you could certainly use restful access your resources
as well, but it's all up to you. The framework makes no
suggestions. You can unroll any URL mapping scheme by simply
associating regular expressions in urls.py with callback view
functions:

{% highlight python %}
from django.conf.urls.defaults import patterns, include, url

urlpatterns = patterns('',
    url(r'^$', 'djangodemo.views.home', name='home')
    url(r'^users', 'djangodemo.view.users', name='list_users'))

{% endhighlight %}

An url is mapped to the callback function, which in turn either renders a
template or directly returns some Http response.

#### Free admin

Django has a built-in support to generate an admin UI for your
website. This is a very useful feature indeed and is supported in
Rails as well through plugins (I've mentioned the one I like the
best).

#### Database migrations

One of the few gripes I have with stock Django is that it doesn't
offer an alternative to Rails's migrations. Luckily there is
[South](http://south.aeracode.org/) - an extension that provides a
simple, stable and database-independent migration layer to prevent all
the hassle schema changes over time bring to your Django
applications. I highly recommend it to everyone planning to use
Django.

#### JavaScript and AJAX

Unlike Rails, Django doesn't bundle any JavaScript libraries. You have
to pick a JavaScript framework yourself (which a trivial process). The
AJAX support in Django is both basic and extremely powerful in the
same time - request.is_ajax(). What this means is that you can check
if a request was regular or an AJAX request and respond
accordingly. You don't need much more than that. More details can be
found [here](https://code.djangoproject.com/wiki/AJAX).

#### The great divide

Some of you probably know that Python is currently at a bit of a
crossroads. Python 2.x was the stable Python version for many years,
but recently it was replaced by Python 3.x. Python 3.x is all around
great in my personal opinion, but unfortunately it's backward
incompatible with the older 2.x series. For that reason very few high
profile projects still don't support it - Django is one such
project. The current version 1.3 require at least Python 2.4 and will
run with every Python up to 2.7. This is a bit of a disappointment
since you'll be missing on a few very cool new features. On a more
positive note Python 2.7 did backport some goodies from Python 3, so
not all is lost. I've read (at totally unofficial places) that Django 2.0 will be targeting Python 3
and I expect it will be available in about a year.

#### Deployment

Python is quite mature technology and offers you a nice array of
deployment options - Apache, Nginx and my favorite - Google App
Engine. Python, being one of the two supported languages on the App
Engine (the other one is, of course, Java) makes it very easy to deploy
Django apps on the App Engine (though you'll need the Django support
for non-relational databases to be able to use it).

The also the possibility to deploy Django apps on Java or .Net
infrastructure using Jython or IronPython.

## Community

When you're selecting the technology for a major project you have to
make sure that the technology is in good shape - there is a solid
community around it, there is no lack of support, innovation and
deployment options.

Both
[Google trends](http://www.google.com/trends?q=ruby+on+rails%2C+django+python)
and stackoverflow.com (by the number of question about tagged with
django or rails) indicate that Rails currently has larger
community than Django.

I haven't had any direct communication with the Django community yet,
but I've found a lot of excellent resources about Django on-line.

Rails has one of the most vibrant, passionate and innovative
communities. I've had contact with a lot of people from the Rails
community and I'm certain that it has played a tremendous role in
Rails's growth.

## Tooling

Traditionally Ruby & Python hackers have been working with just a
powerful programmer's editor like Emacs, vim or TextMate. While there
is nothing inherently wrong with this approach (I'm an avid Emacs user
myself), I do find IDEs quite helpful when working on larger code
bases, with their trademark features such as intelligent
autocompletion (aka intellisense), safe refactorings, on-the-fly syntax checking, etc. So
here's what we've got:

- [RubyMine](http://www.jetbrains.com/ruby/) - hands down the best Ruby and Rails IDE I've ever
  used. The [list of features](http://www.jetbrains.com/ruby/features/index.html) is epic as is the quality of the
  project. It support Rails 3, git, RSpec, Cucumber, sass, haml and
  many other cool Ruby/Rails related technologies. Sure, it's a
  commercial project, but is priced very reasonably.
- [Aptana Studio](http://www.aptana.com/) - a Web development IDE,
  built on top of the Eclipse platform. Among many other features it
  supports Ruby on Rails.
- [Komodo](http://www.activestate.com/komodo-ide) - an IDE focusing on
  dynamic programming language. Great support for both Django and
  Rails development.
- [PyCharm](http://www.jetbrains.com/pycharm/) - from the same company that develops RubyMine, PyCharm
  is the king of IDEs when it comes down to Python. It has full
  featured Django support - there is even autocompletion in the Django
  templates.
- [PyDev](http://pydev.org/) - an Eclipse plug-in for Python and Django development.

I have to admit I'm totally biased. Having been a long time Java
developer I've grown extremely fond of the exceptional IntelliJ
IDEA. RubyMine and PyCharm are both based on the IntelliJ platform and
bring to the Ruby and Python developers much of the might and magic of
IDEA. There are both commercial products, but their price tags are
quite low and their quality is great - highly recommended.

I'm not affiliated in any way with any of these products - I just
happen to like them that much.

## Resources

The are LOTS of resources about Rails and Django on-line. Here are
just my favorites.

#### Rails

* [Rails Guides](http://guides.rubyonrails.org/) - best short
  introduction to Rails ever. Immediately updated for new Rails
  versions, fantastic starting point for any aspiring Rails developer.
* [Rails Tutorial](http://ruby.railstutorial.org/) - best Rails 3 book
  on the market and it even has a free on-line edition. Nice follow up
  of the Rails Guides.
* [RailsCasts](http://railscasts.com/) - Ryan Bates in true Ruby
  hero. He has compiled a unique set of high quality Rails screencasts
  that often illustrate some advanced techniques. And they are all
  free. We all owe a very big "Thanks!" to Ryan.

#### Django

* [Official Docs](https://docs.djangoproject.com/en/1.3/) - best
  official project documentation I've read. It's actually so good,
  that I never (well - almost never) bothered to look for anything else. All my questions
  were answered by the official documentation.

## Epilogue

Choosing Django or Rails is basically a win-win situation - you cannot
go wrong. There are too many similarities between the frameworks and
the differences are not something paramount.

Rails places a heavy emphasis on convention over configuration,
provides you with more defaults and does a can do a lot of heavy
lifting for you automagically.

Django on the other hand let's you specify most configuration details
yourself, without making the configuration burdensome (like that of
older Java web frameworks).

Rails has always been leading on the way of innovation - constantly
integration some of the latest and greatest technologies around
(recent examples being jQuery, Coffee Script and SASS). From time to
time backward compatibility is sacrificed for the greater good, so
that is something that you should consider as well.

Django is certainly much more conservative framework as far as
backward compatibility is concerned - after all it still support
Python 2.4.

I guess in the end the choice really boils down to two things - whether you
like Ruby or Python better and whether you like the defaults imposed
to you by Rails.

I've planned to write a much longer and detailed article, but it's
summer here and it's sunday and I'd rather go out and drink a few
beers with my friends. Hopefully you've enjoyed the article. I'll try
to expand it a bit in the coming days.

P.S. Btw, in case you're wondering - we've picked Rails for our
company's projects. It was a very close call, though, since I
really liked a lot of aspects of Django as well.
