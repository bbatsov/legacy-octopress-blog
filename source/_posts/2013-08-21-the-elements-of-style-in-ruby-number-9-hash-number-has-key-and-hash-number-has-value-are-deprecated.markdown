---
layout: post
title: "The Elements of Style in Ruby #9: Hash#has_key? and Hash#has_value? are deprecated"
date: 2013-08-21 17:04
comments: true
categories:
- Ruby
- Style
---

One can often find similar code in the wild:

``` ruby
some_hash.has_key?(some_key)
```

`has_something?` predicates are not idiomatic in Ruby and
`Hash#has_key?` and `Hash#has_value?` are nothing, but remnants of the
early days of Ruby. In fact, according to Matz, they are
[deprecated](http://blade.nagaokaut.ac.jp/cgi-bin/scat.rb/ruby/ruby-core/43765)
in favor of `Hash#key?` and `Hash#value?`.

The above snippet should look like:

``` ruby
some_hash.key?(some_key)
```

As usual - you can use [RuboCop](https://github.com/bbatsov/rubocop)
to identify and fix such shortfalls of your code.
