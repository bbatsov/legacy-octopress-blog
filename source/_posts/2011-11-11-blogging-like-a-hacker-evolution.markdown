---
layout: post
title: "Blogging Like a Hacker: Evolution"
date: 2011-11-11 08:52
comments: true
categories:
- Octopress
- Jekyll
---

## Prelude

I've started my personal blog some three years ago. Back then in was
hosted on [wordpress.com](http://wordpress.com) and was called
devcraft.wordpress.com. I had a lot of interesting (at least to me)
topics to write about on my mind, but I was immediately faced with a
serious problem - I felt very uncomfortable writing posts in a small
text area, using the primitive editing capabilities of a web
browser. Ordinary decent hackers love and value two tools above all
else - their text editor and their shell. And we love solving problems
automatically with clever programs and scripts, instead of manually.

I knew the only way to ever start writing, like I intended, to was to
actively involve them in the process. So here my story begins...

<!--more-->

## In Emacs We Trust

My editor happens to be Emacs and I've started to look for ways to
blog without leaving its beloved frame. They were several options:

* Use some browser extension that fires up Emacs when editing text
  areas. For instance in Google Chrome there is the extension
  [Edit with Emacs](https://chrome.google.com/webstore/detail/ljobjlafonikaiipfkggjbhkghgicgoh).

* Use [org-mode](http://orgmode.org/worg/org-blog-wiki.html) to write my posts.

* [Emacs Muse](http://mwolson.org/projects/EmacsMuse.html) was another
  option. Emacs Muse is an authoring and publishing environment for
  Emacs. It simplifies the process of writings documents and
  publishing them to various output formats. Muse uses a very simple
  Wiki-like format as input. Muse consists of two main parts: an
  enhanced text-mode for authoring documents and navigating within
  Muse projects, and a set of publishing styles for generating
  different kinds of output.

* Use some Emacs mode, like
[weblogger-mode](http://www.emacswiki.org/emacs/WebloggerMode), that
allows to write and publish WordPress (amongst others) entries directly from Emacs.

All these options had their merits, but they also had their
shortcomings. For one - there is only one writer's markup that I
really enjoy and this is [Markdown](http://daringfireball.net/projects/markdown/). This probably has something to do
with the fact that I've written quite a lot of stuff in GitHub and
Assembla using it. I also wanted the ability to easily include syntax
highlighted code snippets (since I generally write about programming)
and handy way to manage blog updates - preferably via git. I push
something to my repo and voila.

At the time I couldn't make up my mind and my blog was left with a few
quite short posts, due to my inability to withstand being in wordpress
for any prolonged period of time.

Then something extraordinary happened in the beginning of this
year. I've stumbled upon the post
["Blogging Like a Hacker"](http://tom.preston-werner.com/2008/11/17/blogging-like-a-hacker.html)
by GitHub's co-founder Tom Preston-Werner (aka mojombo). It seemed
that other people had exactly the same problem as me. It also seemed
they were more determined to do something about it.

## Along Comes Jekyll

Long story short, Tom had written a blog aware static site generator,
called [Jekyll](https://github.com/mojombo/jekyll) in Ruby. Jekyll
posts are simply Markdown or Textile files and the
[Liquid templating language](http://liquidmarkup.org/) is used to
enhance the posts in their post-processing phase. Code highlighting?
Jekyll (and pygments) has got your back. Nice, ah? There is
support for various layouts and here's be best part - you could put
your blog in a GitHub repo and deploy automatically to GitHub Pages.

I instantly fell in love with Jekyll and as you can see from my
archive I've finally wrote some nice (arguably) & long articles - like I've
originally intended.

While I was mostly happy with Jekyll there were a few things that
bothered me with it:

* You have to design your layouts yourself. While this is generally
  fine if you have a sense for design, when you're someone like me
  that could yield some pretty ugly designs. I was so out of ideas
  that I designed my Jekyll layout to look like my Emacs (down to the
  Zenburn color theme) for which I got a lot of flak.

* Maruku is a really crappy Markdown processor. I wished something
  like RedCarpet was the default and that fenced code blocks (ala
  GitHub) were the default option for code highlighting. Not that you
  can't replace Maruku with Kramdown or RedCarpet, but still. You'd
  also have to patch Jekyll to run albino on the markdown files to get
  the highlighting to work with the fenced blocks.

* You have to do some really boring stuff like Disqus integration,
  twitter integration, etc manually (or at least you have to manually
  install some plugins).

* You have to unroll your own deployment scripts, since Jekyll doesn't
bundle any. Trivial task, but annoying non-the-less.

So there you have it - Jekyll is very nice, but it's also very
barebone. My single biggest gripe with Jekyll, however, is that being
engineered by a GitHub guy it doesn't support out of the box the
GitHub flavored Markdown. At some point as I was seriously
contemplating starting a new static site generator, similar to Jekyll,
that supported only RedCarpet as the Markdown processor and by
extension - the GitHub flavoured Markdown. It would have some nice
default theme and very reasonable default settings for use in a
blog. Google Analytics, Twitter, Disqus would be supported out of the
box. But I never got to writing it since just before I started I was
introduced to Octopress...

## Octopress is Jekyll with Batteries Included

Emacs users are typically portrayed like this:

{% img /images/articles/emacs_user.jpg %}

I was naturally amused by the Octopress name.

First and foremost Octopress is Jekyll with batteries included. Some
of the nicer things include:

* A semantic HTML5 template
* A Mobile friendly responsive (320 and up) layout (rotate, or resize your browser and see)
* Built in 3rd party support for Twitter, Google Plus One, Disqus Comments, Pinboard, Delicious, and Google Analytics
* An easy deployment strategy using Github pages or Rsync
* Built in support for POW and Rack servers
* Easy theming with Compass and Sass
* A Beautiful Solarized syntax highlighting (though not as beautiful
  as the Zenburn-one I'm about to release soon)

And did I mention that there are a lot of nice plugins included?

The default theme is quite nice, but you'd probably want to tweak it a
bit (I still haven't - but my sense of design is nonexistent). It's
very easy to modify the theme.

I could go on and write a lot about Octopress, but there is no need to
do so. Go visit the official [web site](http://octopress.org) - it has fantastic
documentation.

## Moving from Jekyll to Octopress

Mostly trivial. I've just copied my old Markdown posts, adjusted the
headings and the code blocks. And in the end all I had to do was:

``` bash
$ rake generate
$ rake deploy
```

## Epilogue

I love Octopress! I used to be a sad blogger and now I'm a happy
blogger. If you're feeling like I felt - you should definitely give it
a shot. I'll probably do a few follow up articles with some tips &
tricks I've picked along the way with Octopress.
