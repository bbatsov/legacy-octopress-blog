---
layout: post
title: "clojure-mode 3.0"
date: 2014-09-05 15:15
comments: true
categories:
- Clojure
- Emacs
---

[clojure-mode](https://github.com/clojure-emacs/clojure-mode) 3.0 is out!

It's one of the most ambitious releases in recent times and brings
much improved font-locking across the board.  Other notable changes
include dropping support for Emacs 23 (CIDER doesn't support it
either) and removing some deprecated features (most notably the
functionality for switching between code and its test; see
[Projectile](https://github.com/bbatsov/projectile) for an awesome
replacement of the old feature).

An extensive list of the changes is available [here](https://github.com/clojure-emacs/clojure-mode/blob/master/CHANGELOG.md).

This version also marks the introduction of an automated test suite
(currently it consists mostly of font-lock tests), which should make
it easier to do changes in the future.

Next step - indentation improvements and decoupling `clojure-mode`
from `lisp-mode`.  Both tasks are related. We've been deriving much
from `lisp-mode` since day 1 and this has worked reasonably well so
far, but the truth is that Clojure is not Common Lisp (or Emacs Lisp
for that matter) and would benefit from a more refined syntax table,
indentation rules, etc.

When (if) this will happen?
Sadly, I have no idea... Help is definitely welcome! If you
don't have the time to help out with code or docs you can still support my
work on `clojure-mode` (and all my other projects) via
[gratipay](https://www.gratipay.com/bbatsov).

[![Support via Gratipay](https://cdn.rawgit.com/gratipay/gratipay-badge/2.1.3/dist/gratipay.png)](https://gratipay.com/bbatsov)

That's all for now, folks! Enjoy the new `clojure-mode`!
