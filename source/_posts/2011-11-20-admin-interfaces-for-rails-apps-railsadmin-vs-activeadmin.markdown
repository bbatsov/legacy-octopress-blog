---
layout: post
title: "Admin Interfaces for Rails Apps: RailsAdmin vs ActiveAdmin"
date: 2011-11-20 09:24
comments: true
categories:
- Ruby
- Ruby on Rails
- ActiveAdmin
- RailsAdmin
---

## Prelude

Often in comparisons between [Django](https://www.djangoproject.com/)
and Rails, one of the Django advantages being cited is the automatic
admin interface you get for free out-of-the-box there.

I guess a lot of people don't know that there are similar solutions for
Rails, although they are not included in the standard
distribution. Currently the two most prominent admin UI 'frameworks' are
[RailsAdmin](https://github.com/sferik/rails_admin) and [Active Admin](http://activeadmin.info/).

While they are both shooting to solve the same problem, they do it in
a very different way. Many new users are quite confused what
advantages/disadvantages one has over the other (and vice versa) and
that's the reason I'm writing this article right now - to clarify a
few vague points and to help people choose the framework most
appropriate for the task at hand.

<!--more-->

## RailsAdmin

RailsAdmin started its life as a port of MerbAdmin to Rails 3 and was
implemented as a Ruby Summer of Code project by Bogdan Gaza with
mentors Erik Michaels-Ober, Yehuda Katz, Luke van der Hoeven, and Rein
Henrichs. The project is self described as _a Rails
engine that provides an easy-to-use interface for managing your
data._.

Its main features include:

* Display database tables
* Create new data
* Easily update data
* Safely delete data
* Automatic form validation
* Search and filtering
* Export data to CSV/JSON/XML (very handy)
* Authentication (via Devise)
* User action history

RailsAdmin currently supports only ActiveRecord as the ORM. You can
see a live demo of RailsAdmin [here](http://rails-admin-tb.herokuapp.com/).

The current master branch of RailsAdmin targets Rails 3.1.x and it's
naturally aware of the asset pipeline introduced there. Installing
RailsAdmin is a trivial exercise. Just add these deps to your
`Gemfile`:

``` ruby
gem 'fastercsv' # Only required on Ruby 1.8 and below
gem 'rails_admin', :git => 'git://github.com/sferik/rails_admin.git'
```

Afterwards you should run:

``` bash
$ bundle install
$ rails g rails_admin:install
$ rake db:migrate
```

And you're done. RailsAdmin uses internally the tried and true
[Devise](https://github.com/plataformatec/devise) for admin users authentication. If you're already using
devise - you're covered, otherwise RailsAdmin will install it for you.

At this point you can boot your development web server (`rails s`) and
visit the url [localhost:3000/admin](http://localhost:3000/admin) (or whatever port you're running
the dev server on). You'll be able to create admin accounts and after
you log in you'll be presented by an attractive admin dashboard, that
shows you an overview of all the tables in your model.

By default you'll be able to manage every single model in your
app. You'll have to customize the contents of
`config/initializers/rails_admin.rb` to change that default
behavior.

One thing to note is that there are no gem releases of
RailsAdmin. It's still alpha quality software (at least on paper - it's
quite stable actually). I'm generally a bit annoyed to have to track
gems from a git repo, but I understand and respect the developer's
decision on the matter. Hopefully we'll see a stable release of
RailsAdmin soon enough and a gem to go with it.

Another thing to keep in mind is the use case for RailsAdmin - it is
pretty much an automatic backend, that you're not supposed to modify a
lot. In its spirit it's very close to what Django's admin backend
is. RailsAdmin is very smart in determining the relations between
model and supplying forms and show views that express them properly.

Unfortunately not all relationships are represented correctly and
modifying the form builders in RailsAdmin is no walk in the
park. Another minor annoyance is that CarrierWave is not supported out
of the box so you have to do some manual tinkering in the RailsAdmin
initializer to make it work.

Some of the nicer touches in RailsAdmin include basic integration with
CKEditor (a rich WYSIWYG editor) and an user action feature, which
helps keep track of who did what. I wouldn't mind seeing some mention of
TinyMCE as an alternative to CKEditor in the docs, since it's considered more
robust by many (yours truly included).

The docs themselves are just a big README in the project's github
repo. While they feature most of what you'll need to know about
RailsAdmin, having them organized in a nicer way (something that the
guys behind Active Admin have done) wouldn't hurt.

## Active Admin

Active Admin is the other big Rails admin UI framework, developed by
Greg Bell. Its official web site describes it like this:

{% blockqoute %}
Active Admin is a Ruby on Rails plugin for generating administration
style interfaces. It abstracts common business application patterns to
make it simple for developers to implement beautiful and elegant
interfaces with very little effort.
{% endblockquote %}

Active Admin is of course Rails 3.1 ready, plays nice with the asset
pipeline and has great documentation on its official web site. There
also a very nice [introductory screencast](http://railscasts.com/episodes/284-active-admin) by Ryan Bates from RailsCasts.

Getting started with Active Admin is just as easy as getting started
with RailsAdmin. You just need to add a dependency to your `Gemfile`:

``` ruby
gem 'activeadmin'
```

And to a few command line incantations afterwards to seal the deal:

``` bash
$ bundle install
$ rails g active_admin:install
$ rake db:migrate
$ rails s
```

Fire up your favorite browser and visit
[localhost:3000/admin](http://localhost:3000/admin). The default username is
*admin@example.com* and the default password is _password_. You'd
probably be surprised to see an empty dashboard and absolutely no
models that you can administer. Active Admin takes a totally different
approach compared to RailsAdmin. Here nothing happens automatically -
you have to customize your dashboard yourself and you have to register
the models you'd be administrating with the following command:

``` bash
$ rails g active_admin:resource ModelName
```

This will create a file named `app/admin/model_name.rb` where you can
tinker with looks of the resource's index, form and show view.

And here comes Active Admin's core feature - it's immensely easy to
customize anything in the Admin UI. The forms used to create and
update model records are simple Formtastic forms (the same Formtastic
forms you're probably already using throughout the rest of your
apps):

``` ruby
ActiveAdmin.register Post do
  form do |f|
    f.inputs "Details" do
      f.input :title
      f.input :published_at, :label => "Publish Post At"
      f.input :category
    end
    f.inputs "Content" do
      f.input :body
    end
    f.buttons
  end
end
```

Rendering a partial for the form is also supported.

Active Admin features an elegant DSL to express the index and the show
views. Here's an example of index table for a fictional Course
Management app:

``` ruby
ActiveAdmin.register Course do
  index do
    column :id
    column :title
    column :start_date
    column :end_date
    column :created_at
    column :updated_at
    default_actions
  end
end
```

The `default_actions` method invocation here is important - without it
you'll be missing the action buttons in the last column of the index
table.

Here's an example of a show view:

``` ruby
ActiveAdmin.register Post do
  show do
    h3 post.title
    div do
      simple_format post.body
    end
  end
end
```

Alternatively you can forgo the Arbre HTML DSL and render a partial like this:

``` ruby
ActiveAdmin.register Post do
  show do
    # renders app/views/admin/posts/_some_partial.html.erb
    render "some_partial"
  end
end
```

The documentation is very well written and quite extensive so I
wouldn't go into many details here (remember DRY). The only issue I've
had with Active Admin so far is not related to Active Admin directly -
the latest gem release still depends on the old Formtastic 1.3 and I
happen to use Formtastic 2.0 in all of my apps. Luckily the master
branch is already using Formtastic 2.0, so all you have to do if you
have this problem is to use the gem from git:

``` ruby
'activeadmin', git: git://github.com/gregbell/active_admin.git
```

If you're reading this article after the release of Active Admin 0.4
(which should happen any day now) - you don't have to do this.

## Which Should You Use

The answer to that question depends on your needs for a particular
project.

RailsAdmin is still alpha. Unstable developments are made in topic branches
and master is supposed to be as stable as possible. RailsAdmin is not an admin scaffolder as is
Active Admin. It's an automatic backend. It's goal is to provide a full
access to your data, with maximum of defaults extracted from
application's ORM/ActiveModel, a DSL to customize those, and hooks for
third-party projects (Cancan/Devise/Paperclip/CKeditor) to enrich the
experience. Granularity is
higher in RA. You are not supposed to access FormBuilder the way you
would with Active Admin and Formtastic. RailAdmin says here _It's in the dev field, not
configuration_. Still, the current blackbox has some flaws, discrepancies
and uncovered areas that its developers are currently addressing.

Active Admin basically does things the other way around. You're
totally supposed to tweak every aspect of the Admin UI - but tweaking
those aspects is very very easy. If you're looking for a heavily
customized Admin UI solution - Active Admin is certainly the way to
go. It's not an automatic admin backend by any means - it's more or
less a framework that simplifies the creation of admin UIs.

In terms of popularity it seems that RailsAdmin is a bit more popular
right now. I consider the GitHub watchers of a project to be a fairly
accurate measurement of its popularity and as of the time of this
writing RailsAdmin has 2539 compared to 2127 for Active Admin. You
have to consider the fact that RailsAdmin has been out in the open a
bit longer. Active Admin is rapidly closing this gap, however, and I
expect it to surpass RailsAdmin in a month or two.

My personal recommendation is to start by trying RailsAdmin - if it
covers your use cases, you'd do well to simply use it instead of
pouring additional effort into creating a similar UI with Active
Admin. If you need heavily customized admin UI, however, you'd
probably do well to start with Active Admin in the first place, since
after all - it was designed for such scenarios.

## Epilogue

Having used both RailsAdmin and Active Admin with real projects I can
tell you that they serve a different purpose - the
admin UI generated by RailsAdmin is quite usable by default and might
be used with very little changes. Active Admin's admin UI generally
requires manual tweaking to achieve the same effect. On the other hand
Active Admin was developed with manual customization in mind at it's
very easy to do such changes there. Modifying the forms in RailsAdmin
was definitely a less pleasant experience (not to mention stuff like
CarrierWave integration).

While there are some people urging the projects to merge I think that
would be a terrible idea. Aside from the technical difficulties of
merging separate projects sharing no common codebase, I do think diversity
matters. Rails has virtually no alternatives (in Rubyland) and that is bad for
business, since competition always drives innovation. I'd love to see
both projects evolve in their current directions (and stabilize along
the way).

So what are you waiting for? Give them both a shot and share your
experience in the comments section! :-)
