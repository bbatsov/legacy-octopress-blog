---
layout: post
title: "Emacs Dev Kit"
categories:
- Programming
- Emacs
---

During the past few months I've been working on a project to convert
my vast Emacs configuration into something generally useful and
self-contained that could help the general software engineer. Thus the
[Emacs Dev Kit](https://github.com/bbatsov/emacs-dev-kit) was
born. Conceptually it's similar to the older
[Emacs Starter Kit](https://github.com/technomancy/emacs-starter-kit)
and it even shares a bit of code with it. The Emacs Dev Kit, however,
target more programming languages and features more
customizations/enhancements.

EDT relies on ELPA for packages that are available there and packages
everything else locally. At some point I've played with the idea of
using el-get instead, but I had a lot of problems with it and thought
that using only ELPA would be better since it would be part of
Emacs 24. Everything is tested only on the latest version of GNU
Emacs(currently 23.2). I've tried to do everything in the most
efficient and modern way - for instance SLIME is supposed to be
installed via Quicklisp so it could be easily updated without waiting
for a new version of the EDK. 

EDK currently offers enhanced(well, I know that this is subjective,
but it feels enhanced at least to me) support for the following
languages:

* C/C++
* Clojure
* Common Lisp
* Emacs Lisp
* Haskell
* Java
* LaTeX
* Perl
* Prolog
* Python
* Ruby
* Scala
* Scheme
* XML

It also offers an advanced ERC configuration(so that you can ask your
questions on #freenode), extended keybindings and lots of general
purpose utility functions.

EDT goes a step further and even includes a different color-theme by
default - zenburn. You can turn it off easily of course, but I have
the feeling that many programmers will appreciate its eye strain
reducing qualities.

The project is still very young and mostly untested. I'd be thankful
for feedback, bug reports and suggestions.
