---
layout: post
title: "The Elements of Style in Ruby #14: Variable Interpolation"
date: 2014-08-13 16:27
comments: true
categories:
- Ruby
- Style
---

Most experienced Rubyists probably know that there are two ways to interpolate instance, class and global variables into
strings.

``` ruby
# compact notation (works only for instance/class/global vars)
"this is #$some_var"

# standard notation (works for any expression)
"this is #{$some_var}"
```

As you've noticed you can leave out the `{}` which can't be left out for any other expression. Some people find this
interpolation syntax concise and elegant, but I'll argue that it should be avoided. Here's why:

* You can't use this notation in every possible scenario:

``` ruby
# this is fine
puts "#{@variable}string_straight_after_without_space"

# but this means something totally different
puts "#@variablestring_straight_after_without_space"
```

This means that using the compact notation only when applicable forces you to introduce some inconsistency in your code.
This is rarely good...

* You're using different notations for the same basic operation (interpolation), without getting anything in return.
That's not the same with semantic use of single and double quoted strings or `fail` and `raise`.

``` ruby
# using compact
"this is #@x"
"this is #{x}"

# using standard
"this is #{@x}"
"this is #{x}"
```

* It's easy to make a mistake in the context of a regular expression
(as interpolation works in regexp literals).  Recently I saw the
following regexp - `/[0-9.(),;:!?%#$?\x27\x22_+=\\\/\-]*/`. There's a
subtle problem with it, that's not obvious (unless you have a good
editor, that is). The sequence `#$?` is interpreted as interpolation
of the global variable `$?` (a.k.a. `$CHILD_STATUS`) and this regexp doesn't work as intended.

This scenario shows that the syntax was ill-conceived.

* Non-experience Rubyists probably don't know about the compact interpolation notation.
Few books and tutorials mention it these days, so using it your code will confuse at least
some of the people reading it.

-----------

It seems to me that Ruby will be better off without a special syntax
for variable interpolation. Ideally it would be removed in Ruby 3 and
we'll have one less thing to worry about in our Ruby code.

That's all for today, folks!

As usual I'm looking forward to hearing your thoughts here and on
[Twitter](http://twitter.com/bbatsov)!
