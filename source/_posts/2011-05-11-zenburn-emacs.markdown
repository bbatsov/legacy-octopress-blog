---
layout: post
title: "A new Zenburn theme for Emacs"
categories:
- Emacs
---

[Zenburn](http://slinky.imukuppi.org/zenburnpage/) is a popular colour theme for
vim, developed by Jani Nurminen. It's my personal
belief (and probably that of many of its users I presume) that it's one of the
best low contrast themes out there and that Zenburn is exceptionally
easy on the eyes. Btw, I love Zenburn so much that I've even created a
[Zenburn theme for Jekyll](https://github.com/bbatsov/blog/blob/master/css/syntax.css) to be able to use for my blog.

The project was originally
[ported to Emacs](https://github.com/dbrock/zenburn-el) by Daniel
Brockman, but it seems that he has lost interest in it recently - very
few updates has been published by him in the past few years. This is
the reason why I gathered all improvements that I could find laying
around the Internet and applied them to the last official Zenburn
version, effectively starting
a [fork of the project](https://github.com/bbatsov/zenburn-emacs/blob/master/zenburn-legacy.el). So far, so good...

Daniel's version of Zenburn, however, had reached a state in which it took me
too much to make improvements to it - since a lot of users had direct access
to modify it everything in it was in complete disarray - it's full of
uses of colours that were not defined by the original zenburn,
questionable coding practices and inconsistent theming of
faces. Yesterday I decided to take a closer look at the code of the
theme and clean it up a little - 20 minutes later I was writing [a new
zenburn theme from scratch](https://github.com/bbatsov/zenburn-emacs/blob/master/zenburn.el). I decided that making everything from
the start will probably be less effort anyways. 

I've added enough faces in the new theme to make it usable for most
users and I'll (hopefully) continue to improve the theme and expand
the supported modes constantly. If you're interested - give it a try!
If you're unhappy with something - create an issue in GitHub (or even
better send me a pull request with your suggested improvements).

It's my desire to make the new [Zenburn for Emacs](https://github.com/bbatsov/zenburn-emacs) just as good as the original.
