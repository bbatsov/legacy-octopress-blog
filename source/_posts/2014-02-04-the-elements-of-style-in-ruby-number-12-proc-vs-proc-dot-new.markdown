---
layout: post
title: "The Elements of Style in Ruby #12: proc vs Proc.new"
date: 2014-02-04 16:20
comments: true
categories:
- Ruby
- Style
---

People are often confused about the fact that there are two ways to created `proc`s in Ruby -
via `Kernel#proc` and `Proc.new`. Let's see them in action:

``` ruby
Proc.new { true }
# => #<Proc:0x007fe35440a058>

proc { true }
# => #<Proc:0x007fe35440a059>
```

Hmmm, it seems we get exactly the same results... While this is true
on Ruby 1.9+, this was not always the case.

In Ruby 1.8, `Kernel#proc` is actually a synonym for `Kernel#lambda`
which was extremely confusing, since as we all know `lambda`s an
`proc`s differ in
[subtle ways](http://stackoverflow.com/questions/626/when-to-use-lambda-when-to-use-proc-new). Luckily
sanity prevailed and Ruby 1.9 made `Kernel#proc` a synonym for
`Proc.new` instead.

At this point, however, people couldn't use `Kernel#proc` anymore if they
wanted to write code that's behaving in the same way on both Ruby 1.8
and Ruby 1.9 and the use of `Kernel#proc` was generally discouraged.
Thankfully Ruby 1.8 is now dead and buried and there's no reason to prefer
`Proc.new` over `Kernel#proc` anymore.  As a matter of fact - you
should probably be using only `Kernel#proc` as it's more concise and
it's symmetrical to `Kernel#lambda`.

``` ruby
lambda { true }
# => #<Proc:0x007fe35440a058 (lambda)>

proc { true }
# => #<Proc:0x007fe35440a059>
```

By the way, given `proc`'s fairly counter-intuitive behavior regarding `return`, you should probably
use `lambda`s most of the time.
