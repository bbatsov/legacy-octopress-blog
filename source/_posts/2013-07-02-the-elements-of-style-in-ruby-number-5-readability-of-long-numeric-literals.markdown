---
layout: post
title: "The Elements of Style in Ruby #5: Readability of long numeric literals"
date: 2013-07-02 15:01
comments: true
categories:
- Ruby
- Style
---

Today's topic is the following rule from the [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide):

> Add underscores to large numeric literals to improve their readability.

Most of the programs we write feature a substantial number of numeric
literals(e.g. `10`, `0.34`, `0b1010`, `0123`, `0xCAFE`). There is nothing
strange or unusual about that. From time to time, however, those literals are pretty long:

```
MAX_SIZE = 10000000000
DEVIATION = 0.2343434343
BIT_MASK = 0b100101010101
```

I'm pretty sure most of you would have pretty hard time to quickly
digest a number written in this way - lots of digits and no separators
between them to help us discern the number's `structure`. At this
point `_` makes a dramatic appearance and comes to the rescue:

```
MAX_SIZE = 10_000_000_000
DEVIATION = 0.2_343_434_343
BIT_MASK = 0b1001_0101_0101
```

The addition of a few `_` improves the readability of those huge literals a ton!

The underscores we add to numeric literals are ignored by `Ruby`:

``` ruby
100_000
# => 100000
```

As you can see from the preceding example nothing's lost or changed -
we've only gained readability and eased the parsing burden on our
brains.

Obviously we should not overdo `_`:

``` ruby
# short literals are pretty readable on their own
# bad
1_00

# good
100
```

Personally, when dealing with decimal literals, I tend to use `_` for
numbers with at 5 least digits(e.g. `11_948`). The number of digits to separate with
`_` depends on the numeric base - in decimal it makes sense to group
digits by 3(`1_000_000`), in binary by 4(`0b1111_1010_1110`), etc.

That's all for today folks! Hope I managed to convince at least a few
of you of the benefits of using underscores in your long numeric literals.

As usual I'm looking forward to hearing your thoughts here and on
[Twitter](http://twitter.com/bbatsov)!
