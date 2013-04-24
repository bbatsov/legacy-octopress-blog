---
layout: post
title: "RuboCop 0.6.0 released"
date: 2013-04-23 14:46
comments: true
categories:
- Ruby
---

[RuboCop](https://github.com/bbatsov/rubocop) 0.6.0 was just released!
It's RuboCop's biggest and most ambitious release yet.  Here's the
highlights:

* 15 new cops(checks)
* Support for disabling cops locally in a file with `rubocop:disable` comments
* Half a dozen bugs squashed
* Small improvements across the board

I guess the support for disabling cops locally deserves a bit of special treatment.

So here's the basics - you're now allowed to enable/disable certain cops
(checks) and to alter their behavior if they accept any parameters.

One or more individual cops can be disabled locally in a section of a
file by adding a comment such as:

``` ruby
# rubocop:disable LineLength, StringLiterals
[...]
# rubocop:enable LineLength, StringLiterals
```

You can also disable *all* cops with:

``` ruby
# rubocop:disable all
[...]
# rubocop:enable all
```

One or more cops can be disabled on a single line with an end-of-line
comment:

``` ruby
for x in (0..19) # rubocop:disable AvoidFor
```

You can see all the gory details in the
[changelog](https://github.com/bbatsov/rubocop/blob/master/CHANGELOG.md). I hope you'll enjoy RuboCop 0.6.0!
