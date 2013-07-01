---
layout: post
title: "The Elements of Style in Ruby #4: Array#join vs Array#*"
date: 2013-07-01 16:28
comments: true
categories:
- Ruby
- Style
---

Today's topic is the following rule from the [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide):

> Favor the use of `Array#join` over the fairly cryptic `Array#*` with
> a string argument.

`Array#join` and `Array#*` (with a string argument) behave exactly the same:

``` ruby
%w(Bruce Wayne).join(' ')
# => "Bruce Wayne"

%w(Bruce Wayne) * ' '
# => "Bruce Wayne"
```

So, considering they both do the same thing why should you opt to use
`join` instead of `*`? Here's a few reasons:

* `*` behaves totally differently when passed an integer argument:

``` ruby
[1 2] * 3
# => [1 2 1 2 1 2]
```

Personally, I'd expect this to be only behavior of such an operator
method and find the alternative one (with a string argument) to be
pretty much counter-intuitive.

* It's not always clear what `*` means without additional
  context. Take a look at this short snippet:

``` ruby
# a and b are variables
a * b
```

Without some knowledge of `a` and `b` we cannot be certain what this
code is going to do. It's hard even to speculate what the code is
going to do. Obviously better variable names would certainly help, but
the point still stands.

```
a.join(b)
```

While we still cannot be absolutely certain, it's highly likely that `a` is
an `Array` and `b` is a `String`.

* `*` does not carry much of a semantic value in it.

Unlike `String#%`, `Array#*` with a string argument carries pretty
much no meaning. It's absolutely beyond me how this came into
existence. On the other hand the behavior of `Array#*` with an integer
argument is pretty reasonable. Here we see a classic example of the
notion that too much operator overloading can be a bad thing, leading
to some pretty unreadable code. An operator should be employed only
when it's use would add clarity to the code, not take clarity away.

`Array#*` has one thing going for it, however - the fact that few
people know about its use as a substitute for `Array#join`. I hope
they realize that some unknown features are unknown for a reason -
because it's bad idea to make use of them.

As usual I'm looking forward to hearing your thoughts here and on
[Twitter](http://twitter.com/bbatsov)!
