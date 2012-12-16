---
layout: post
title: "Emacs 24.3 introduces native OSX full-screen support"
date: 2012-12-09 13:34
comments: true
categories: 
- Emacs
- OSX
---

One of the most requested Emacs features - native OSX Lion style
full-screen support has finally landed in Emacs 24.3 (due to be
released in a few months). If you're eager to try it out right now
homebrew is your best bet:

``` bash
$ brew install emacs --cocoa --use-git-head
```

Homebrew's devs have even backported the full-screen patch to Emacs
24.2, so if you're not very adventurous you can just do:

``` bash
$ brew install emacs --cocoa
```

Using nightly builds from
[Emacs for Mac OSX](http://emacsformacosx.com/) is a no-go at the
moment, since they seem to be compiling Emacs without the required
compilation flag to enable the full-screen support.

Here's the beast in action:

{% img /images/articles/emacs-full-screen.png %}

This was a short article, but I do hope you'll find it useful.
