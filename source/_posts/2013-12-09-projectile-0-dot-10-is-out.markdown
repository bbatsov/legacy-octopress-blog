---
layout: post
title: "Projectile 0.10 is out!"
date: 2013-12-09 15:26
comments: true
categories:
- Emacs
---

[Projectile](https://github.com/bbatsov/projectile) 0.10.0 is out!

This might come as a surprise for people tracking Projectile's
development, since recent snapshots were using 1.0 as the version
number, so allow me to explain. I've been wanting to release
Projectile 1.0 for a while now, but I felt that without the addition
of _per-project settings_ support and some refinements to the way
_ignoring of files & folders_ currently work, such moniker would be
unjustified. Unfortunately, lately I've been quite busy working on
other projects like [cider](https://github.com/clojure-emacs/cider)
and [RuboCop](https://github.com/bbatsov/rubocop) and I don't have
that much time to work on Projectile, so I kept delaying the 1.0
version.

Recently I decided to release version 0.10 instead, for the benefit of
users of package repos like Marmalade. The minor bump in the version
doesn't mean that 0.10 is not a noteworthy update, though. 5 months of
development and more than a hundred commits from almost a dozen of
developers have really improved the Projectile experience.  It's
easily the biggest update of Projectile, since the project was
conceived.

Some of the highlights include:

* `.projectile` is always taken into account (previously it was consulted only when doing `native` indexing)
* There's now the ability to search for files in a specific directory
* More project types are recognized
* You can search for etags (ctags) in a project
* **The Commander** (a really cool feature inspired from CIDER & SLIME, that I'll show in a bit)
* Dozens of (mostly undocumented in the Changelog) bugfixes

Have a look at the [changelog](https://github.com/bbatsov/projectile/blob/master/CHANGELOG.md) for more details.

And here's the new **Commander** in action:

{% img /images/articles/projectile-commander.gif %}

Basically it gives you a way to invoke many of the Projectile commands
with a single key - `f` for `find-file`, `s` for `switch-project`,
etc. It's very handy when switching projects since with this command
you can always pick a different command to execute in the new
project. By the way, `projectile-switch-project` will now run the
commander, when invoked with a prefix argument (`C-u C-c p s`).
