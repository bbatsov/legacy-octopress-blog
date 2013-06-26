---
layout: post
title: "RuboCop 0.8.0 is out, support for JRuby and Rubinius is in!"
date: 2013-05-28 12:11
comments: true
categories:
- Ruby
---

[RuboCop](http://github.com/bbatsov/rubocop) 0.8.0 is out!

While the version bump is minor, this release represents an almost
total rewrite of the code. We've moved away from MRI's `Ripper` parser
and ported RuboCop to [Peter Zotov](https://github.com/whitequark)'s
fantastic [Parser](https://github.com/whitequark/parser).

What does this mean for users of RuboCop? It means that now both
Rubinius and JRuby are supported (in 1.9 and 2.0 modes). I'd say this
is kind of a big deal! The support for the them should be considered
beta at this point, since they have not yet received extensive field
testing.

And what does the change mean for developers? It's now a lot easier to
comprehend RuboCop's source code, lowering the bar for contributions
immensely.

What's coming down the road for 0.9.0? We have two big changes
planned - providing an auto-fix functionality(meaning RuboCop will be
able to fix on its own some of the problems detected) and providing
more precise diagnostic messages(a-la `clang`).

The changelog for 0.8.0 is available [here](https://github.com/bbatsov/rubocop/blob/master/CHANGELOG.md).

Stay tuned for more!
