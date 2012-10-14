---
layout: post
title: "Rails Tip #1: Use Pry Instead of irb for the Rails Console"
date: 2012-10-14 18:06
comments: true
categories: 
- ruby
- rails
- tip
---

This tip is going to be a really short one. Hopefully by now you've
heard about [pry](http://pryrepl.org/) - a fantastic `irb`
replacement, that somewhat reminds me of the mighty Lisp REPLs. What
you might not know is how to hook it into Rails so that the `rails
console` (a.k.a. `rails c`) command would fire a pry shell instead of
an irb one. There are several ways to do so, but I find one
particularly straightforward - the awesome little gem
[pry-rails](https://github.com/rweng/pry-rails).

So what are you waiting for? Go ahead, install the little sucker and
enjoy your new pry-powered Rails console.

