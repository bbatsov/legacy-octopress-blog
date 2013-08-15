---
layout: post
title: "The Elements of Style in Ruby #8: Know Thy Predicates"
date: 2013-08-14 17:28
comments: true
categories:
- Ruby
- Style
---

I often see people writing code like this:

``` ruby
if x % 2 == 0 ...
```

Obviously `Fixnum#even?` would have been a better choice:

``` ruby
if x.even? ...
```

There is also `Fixnum#odd?` if you need to check for odd numbers.

By the way, there is even a `Numeric#zero?` predicate:

``` ruby
if x == 0 ...

# same as
if x.zero? ...
```

Personally I feel that `x == 0` makes more sense for such simple
numeric checks, but `zero?` is there for those you who think
otherwise.

Another bit of code you'll often see is:

``` ruby
if x > 0 && x < 7 ...
```

While there is nothing particularly bad about that code, I'd argue
that `between?` makes for a nicer (and more OO) alternative:

``` ruby
if x.between?(1, 6) ...
```

Using a range predicate you can also exclude the end value:

``` ruby
if x > 0 && x < 1000 ...

# is the same as
if (1...1000).include?(x) ...
```

When using predicate methods you should be mindful of `nil`
receivers. That's generally not a serious issue in practice but still I'd ask
you to consider this example:

``` ruby
if arr == [] ...
```

It's not equivalent to

``` ruby
if arr.empty?
```

Why so? Because `arr` might be `nil`. So the equivalent code would be:


``` ruby
if !arr.nil? && arr.empty?
```

Of course checking for `nil`s like this is generally not a good idea, but
that's a discussion for some other time.

On a somewhat related note `something.nil?` is generally preferred
over `something == nil`. If you're reasonably sure that `something`
can't have the value `false` you can, of course, simplify things even
further:

``` ruby
if something ...
```

As usual I'm looking forward to hearing your thoughts here and on
[Twitter](http://twitter.com/bbatsov)!
