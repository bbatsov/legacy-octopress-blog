---
layout: post
title: "Ruby Tip #1: Demystifying the Difference Between == and eql?"
date: 2011-11-28 16:54
comments: true
categories:
- Ruby
- Tips
---

Newcomers to Ruby are often confused by the fact the `Object` class
defines three methods related to equality - `==`, `eql?` and
`equals?`. Of the three the one that it's easiest to describe is
`equal?` - it implements what's commonly known as reference equality
check. The method returns `true` only if its receiver (the object upon
the method was invoked) and parameter (the object we're comparing to) are
the same object (Java developers should think of the `==` operator
there).

``` ruby
some_word = "word"
some_other_word = some_word

some_word.equals? some_other_word # true
```

Both `==` and `eql?` implement value equality checks - they are not
interested in whether two variables point to the same object in
memory, but whether two objects are equal in terms of their
values. For instance "cat" and "cat" might very well be two completely
different `String` objects, but they are quite obviously the same as
far as their value is concerned.

``` ruby
"cat".equals? "cat"    # false
"cat" == "cat"         # true
"cat".eql? "cat"       # true
```

What's not immediately obvious is why are there two different
methods that seem to be doing exactly the same thing. The answer is
simple - `eql?` is meant to be used as a stricter version of `==`, if
there is a need for such stricter version.`eql?` most prominent usage
is probably in the `Hash` class, where it's used to test members for equality.

In the `Object` class `eql?` is synonym with `==`. Most subclasses
continue this tradition, but there are a few classes that provide a
different implementation for `eql?`.  Numeric types, for example,
perform type conversion across `==`, but not across `eql?`, so:

``` ruby
1 == 1       # true
1.eql? 1     # true
1 == 1.0     # true
1.eql? 1.0   # false
1.0.eql? 1.0 # true
```

As you can see clearly from this example - `eql?` for `Numeric` classes
requires both objects to be instances of the same class, apart from
having equal values, to return `true`.

If you're wondering about the origins of that convention I should probably
refer you to Common Lisp (one of the languages cited as principle
inspiration for Ruby). Common Lisp has [quite a few equality
predicates](http://eli.thegreenplace.net/2004/08/08/equality-in-lisp/),
dealing with various aspects of equality. I guess I never found `==`
and `eql?` in Ruby particularly confusing, because I knew Common Lisp,
before I started playing around with Ruby.

Hopefully, I've managed to make the difference between `==` and `eql?`
clear. That's some fairly esoteric matter that's not totally
understood by even some fairly experienced Ruby developers.
