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
homebrew is a good option:

``` bash
$ brew install emacs --cocoa --use-git-head --HEAD
```

Homebrew's devs have even backported the full-screen patch to Emacs
24.2, so if you're not very adventurous you can just do:

``` bash
$ brew install emacs --cocoa
```

Alternatively you can install the
[Emacs 24.2.91 pretest](http://emacsformacosx.com/emacs-builds/Emacs-pretest-24.2.91-universal-10.6.8.dmg)
(or a newer pretest/nightly build) from
[Emacs for Mac OSX](http://emacsformacosx.com/). Personally I
recommend this option, since cloning the Emacs git mirror (as homebrew
does) takes like forever.

Here's the beast in action:

{% img /images/articles/emacs-full-screen.png %}

This was a short article, but I do hope you'll find it useful.
