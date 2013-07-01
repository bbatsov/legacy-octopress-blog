---
layout: post
title: "The Elements of Style in Ruby #3: Make sure something is an array"
date: 2013-06-28 15:39
comments: true
categories:
- Ruby
- Style
---

The subject of today's post is the following rule from the
[Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide):

> Use `[*var]` or `Array()` instead of an explicit `Array` check, when dealing with a </br>
> variable you want to treat as an Array, but you're not certain it's </br>
> an array.

Countless times I've seen code like this:

``` ruby
paths = [paths] unless paths.is_a? Array
paths.each { |path| do_something(path) }
```

It seems that `paths` could be either an `Array` object or an object
of some other class. The author of the code needed to make sure
`paths` would be an array so he creates a single element array in the
case `paths` is not already an array.

While the above code works it's not something an experienced Rubyist
would write. The most popular alternative is the use of the mighty splat
operator(`*`):

``` ruby
[*paths].each { |path| do_something(path) }
```

It case you're puzzled by the preceding snippet consider the following example:

``` ruby
elems = 1
[*elems]
# => [1]

elems = [1, 2, 3]
[*elems]
# = [1, 2, 3]
```

Hope that makes clear what's going on.

While I'm extremely fond of this particular usage of `*` I tend to
avoid it, since there is another equally powerful, but more readable
alternative to it - `Kernel#Array`. Here's it in action:

``` ruby
Array(paths).each { |path| do_something(path) }
```

`Array` looks like the name of class, but it's not. It's a totally
normal method defined in the `Kernel` module. There is a whole family
of conversion methods similar to `Array` there - `Array`, `Complex`,
`Float`, `Hash`, `Integer`, `Rational` and `String`. They are all used
for often in practice and we'll probably revisit them in a separate
post somewhere down the road.

The `Array` method operates exactly like `*` - it takes a single argument and
converts it to an `Array` object if necessary:

``` ruby
Array(1)
# => [1]

Array([1, 2, 3])
# => [1, 2, 3]
```

You can also use `*` and `Array` to convert to array other data
composite data structures (like hashes and sets), but that's
irrelevant to today's discussion.

That's all I have for you today, mates. As usual I'm looking forward
to hearing your thoughts here and on
[Twitter](http://twitter.com/bbatsov)!
