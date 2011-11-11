---
layout: post
title: "Blogging Like a Hacker: Evolution"
date: 2011-11-11 08:52
comments: true
categories:
Octopress
Jekyll
---

## Prelude

I've started my personal blog some three years ago. Back then in was
hosted on [wordpress.com](http://wordpress.com) and was called devcraft.wordpress.com. I had a
lot of interesting topics to write about on my mind, but I was
immediately faced with a serious problem - I felt very uncomfortable
writing posts in a small text area, using the primitive editing
capabilities of a web browser. Ordinary decent hackers love and value
two tools above all else - their text editor and their shell.

I new the only way to ever start writing like I intended to was to
actively involve them in the process. So here my story begins...

<-! more ->

## In Emacs We Trust

My editor happens to be Emacs and I've started to look for ways to
blog without leaving my beloved editor. They were several options:

* Use some browser extension that fires up Emacs when editing text
  areas.

* Use org-mode to write my posts.

* [Emacs Muse](http://mwolson.org/projects/EmacsMuse.html) was another
  option. Emacs Muse is an authoring and publishing environment for
  Emacs. It simplifies the process of writings documents and
  publishing them to various output formats. Muse uses a very simple
  Wiki-like format as input.  Muse consists of two main parts: an
  enhanced text-mode for authoring documents and navigating within
  Muse projects, and a set of publishing styles for generating
  different kinds of output.

* Use some Emacs mode that allows to write and publish wordpress
entries directly from Emacs.

All these options had their merits, but they also had their
disadvantages. For one - there is only one writer's markup that I
really enjoy and this is Markdown. This probably has something to do
with the fact that I've written quite a lot of stuff in GitHub and
Assembla using it. I also wanted the ability to easily include syntax
highlighted code snippets (since I generally write about programming)
and handy way to manage blog updates - preferably via git. I push
something to my repo and voila.

At the time I couldn't make up my mind and my blog was left with a few
quite short posts, due to my inability to withstand being in wordpress
for any prolonged period of time.

Then something extraordinary happened this year. I've stumbled upon
the post
["Blogging Like a Hacker"](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)
by GitHub's co-founder Tom Preston-Werner (aka mojombo). It seemed
that other people had exactly the same problem as me. It also seemed
they were more determined to do something about them.

## Along Comes Jekyll

Long story short, Tom had written a blog aware static site generator,
called Jekyll in Ruby. Jekyll posts are either Markdown or Textile
files, the Liquid templating language is used to enhance the posts in
their post-processing phase, there is support for various layouts and
here's be best part - you could put your blog in a GitHub repo and
deploy automatically to GitHub Pages.

I instantly fell in love with Jekyll and as you can see from my
archive I've finally wrote some nice & long articles - like I've
originally intended.

While I was mostly happy with Jekyll there were a few things that
bothered me with it:

* You have to design your layouts yourself. While this is generally
  fine if you have a sense for design, when you're someone like me
  that could yield some pretty ugly effects. I was so out of ideas
  that I designed my Jekyll layout to look like my Emacs with the
  Zenburn color theme.

* Maruku is a really crappy Markdown processor. I wished something
  like RedCarpet has the default and that fenced code blocks (ala
  GitHub) were the default option for code highlighting. Not that you
  can't replace Maruku with Kramdown or RedCarpet, but still. You'd
  also have to patch Jekyll to run albino on the markdown files to get
  the highlighting.
