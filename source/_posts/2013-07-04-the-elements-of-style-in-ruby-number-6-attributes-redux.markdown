---
layout: post
title: "The Elements of Style in Ruby #6: Attributes Redux"
date: 2013-07-04 15:36
comments: true
categories:
- Ruby
- Style
---

Today we'll talk about attributes in Ruby.

Let's start with the following rule from the
[Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide):

> Use the `attr` family of functions to define trivial accessors or mutators.

Everyone who's coded a bit of Ruby knows it's preferable to generate
trivial reader and writer methods via some metaprogramming magic
instead of writing them by hand. The methods from `Module` `attr`,
`attr_reader`, `attr_writer` and `attr_accessor` do exactly that kind
of magic. Here's an example using `attr_reader`:

``` ruby
# bad
class Person
  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
  end

  def first_name
    @first_name
  end

  def last_name
    @last_name
  end
end

# good
class Person
  attr_reader :first_name, :last_name

  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
  end
end
```

Here's `attr_writer` in action:

``` ruby
# bad
class Person
  def initialize(name, name)
    @name = name
  end

  def name=(name)
    @name = name
  end
end

# good
class Person
  attr_writer :name

  def initialize(name)
    @name = name
  end
end
```

`attr_accessor` combines the two:

``` ruby
# bad
class Person
  def initialize(name, name)
    @name = name
  end

  def name
    @name
  end

  def name=(name)
    @name = name
  end
end

# good
class Person
  attr_accessor :name

  def initialize(name)
    @name = name
  end
end
```

Pretty sure none of you has learned anything new at this point. Now we start with the fun part...

How many of you know how `attr` behaves? Are you totally sure? Let's
see what the style guide says about it:

> Avoid the use of `attr`. Use `attr_reader` and `attr_accessor` instead.

`attr`'s behavior changed between Ruby 1.8 and 1.9. In Ruby 1.8 `attr`
created a single _reader_ method. With an optional second boolean argument it
created both a _reader_ and a _writer_ method (a la `attr_accessor`).

``` ruby
# Ruby 1.8
# same as attr_reader :something
attr :something

# creates a single attribute accessor (deprecated in 1.9) - same as attr_accessor :something
attr :something, true

# can't do this
attr :one, :two, :three
```

Note that you cannot pass multiple attribute names to `attr` in Ruby 1.8.

In Ruby 1.9 calling `attr` with an attribute name and a boolean is
deprecated and it now behaves a lot more like `attr_reader`.

``` ruby
# Ruby 1.9
attr :one, :two, :three # behaves as attr_reader
```

Given all this facts it's not a surprise that so many people think
it's a bad idea to use `attr`. I guess if the design of that portion
of the API were up to me I'd have made `attr` behave like
`attr_accessor` from day 1. The name of `attr_accessor` is a bit of a
misnomer since `accessor` is hardly a synonym for **reader and
writer**. Anyways, this is not of particular importance. Off to the
next item on our agenda for today.

Is this something that should have been defined with `attr_reader`?

``` ruby
def something
  @something_else
end
```

Basically it call comes down to whether this is a trivial reader method or not.
Some people would argue that because the name of the instance variable
and the name of the method are not the same - it's not. I'd argue the
opposite case - it is! The name of the method does not change the
semantics. In essence you're simply in need of an alias for the
_default_ attribute reader method:

``` ruby
attr_reader :something_else
alias_method :something, :something_else
```

Boolean attributes are a bit special, since generally we'd like to
have a `?` at the end of predicate method names, but this cannot be done with
`attr_reader/attr_accessor`. Some people would simple hand-code such
methods:

``` ruby
def something?
  @something
end
```

I'd employ `alias_method` again:

```
attr_reader :something
alias_method :something?, :something
```

I wouldn't call one style necessary good or bad - it's more of a personal preference.

One final note - you should use `attr_` only for trivial reader and writer methods (trivial means that
they do not need any defensive copying or pre-update checks).

Consider this:

``` ruby
# attr_reader generates code like this
def something
  @something
end
```

This would expose `@something` to external modifications if it's a
mutable object. To shield yourself from this you can use defensive
copying (or freezing when applicable):

``` ruby
# defensive copying in action
def something
  @something.dup # return a copy of @something
end
```

Same goes for attributes writers. If you have an `age` attribute and you
want to enforce that it should be a positive number you'd generally roll your
own writer:

``` ruby
def age=(age)
  fail 'Age should be a positive number!' unless age > 0

  @age = age
end
```

This post has become way too long, so I'll be wrapping it up. I hope
you've found my musing on the subject of attributes useful.

As usual I'm looking forward to hearing your thoughts here and on
[Twitter](http://twitter.com/bbatsov)!

**P.S.** Happy 4th of July to all my American readers! :-)
