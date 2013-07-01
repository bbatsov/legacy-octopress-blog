---
layout: post
title: "The Elements of Style in Ruby #2: Favor sprintf(format) over String#%"
date: 2013-06-27 13:15
comments: true
categories:
- Ruby
- Style
---

Today's topic is the following rule from the [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide):

> Favor the use of `sprintf` and its alias `format` over the fairly </br>
> cryptic `String#%` method.

`Kernel#sprintf` and `String#%` basically do the same thing - the main
difference is that `sprintf` is generally used as a command(it does
not operate on its receiver) and `String#%` is obviously an instance
method of the class `String`. Here's the two of them in action:

``` ruby
'%d %d' % [20, 10]
# => '20 10'

sprintf('%d %d', 20, 10)
# => '20 10'
```

So, considering they both do the same thing why should you opt to use
`sprintf` instead of `%`? Here's a few reasons:

* `%` takes either a single element or an array of elements as its
  sole argument; `sprintf` consistently takes a variable number of
  arguments.

``` ruby
'%d' % 20
# => '20'

'%d %d' % [20, 10]
# => '20 10'

sprintf('%d %d', 20)
# => '20'

sprintf('%d %d', 20, 10)
# => '20 10'
```

Personally, I dislike such inconsistencies a lot.

* It's not always clear what `%` means without additional
  context. Take a look at this short snippet:

``` ruby
# a and b are variables
a % b
```

Without some knowledge of `a` and `b` we cannot know if we're dealing
with a modulo operation (if `a` and `b` are fixnums), `String#%` or if
`a` is an instance of some other class which has implemented the `%`
method.

With `sprintf` it's always crystal-clear what's going on.

* `%` does not carry much of a semantic value in it.

Sure, it was named so because of the `%` placeholders in the target
string, but people not familiar with that operator will probably be
confused by such odd-looking syntax. `sprintf` on the other hand is
old as time (so people reading your code have probably encountered it
somewhere before) and beside that it's fairly easy to remember that it
stands for `string print formatted` (or something similar). On a
related note - the use of `Kernel%sprintf`'s alias `format` yields
even better readability, since `format` is obviously less cryptic name
than `sprintf` and the same name is employed in many programming
languages (most notably `Java` and many Lisp dialects).


There's one thing about `sprintf/format` that I dislike, though. It
doesn't make that much sense to have such an operation as command in a
OO language like Ruby. Alas, those things are not up to me - I guess
the authors had something in mind when they made that particular
decision about the standard library.

In an ideal world the standard library would have included a
`String#format` method, that took variable number of arguments. For
some reason (unknown to me) - that has not happened (and maybe never
will). For now the use of `Kernel#sprintf` (and `Kernel#format`)
yields the best results when it comes down to code clarity and
consistency. I encourage you to use them (`format` in particular)!

As usual I'm looking forward to hearing your thoughts here and on
[Twitter](http://twitter.com/bbatsov)!
