---
layout: post
title: "Find out where a rake task is defined"
date: 2014-05-30 17:23
comments: true
categories:
- Ruby
- rake
---

Have you ever wondered where a particular rake task is defined? Enter `rake -W` (introduced in `rake` 0.9):

```
$ rake -W db:schema:load

rake db:schema:load                 /Users/bozhidar/.rbenv/versions/2.1.1/lib/ruby/gems/2.1.0/gems/activerecord-4.1.1/lib/active_record/railties/databases.rake:236:in `block (2 levels) in <top (required)>'
rake db:schema:load_if_ruby         /Users/bozhidar/.rbenv/versions/2.1.1/lib/ruby/gems/2.1.0/gems/activerecord-4.1.1/lib/active_record/railties/databases.rake:240:in `block (2 levels) in <top (required)>'
```

You can also invoke `rake -W` without an argument and you'll get a listing of all available rake tasks and their source locations.

Pretty neat, right?
