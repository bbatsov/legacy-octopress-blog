---
layout: post
title: "The Elements of Style in Ruby #11: Invoking Lambdas/Procs"
date: 2013-09-26 17:43
comments: true
categories:
- Ruby
- Style
---

There are whopping 4 ways to invoke a lambda (or a proc) in Ruby:

``` ruby
lambda.call(arg1, arg2)

lambda[arg1, arg2]

lambda.(arg1, arg2)

# works only with one argument lambdas
lambda === arg
```

The last option `Proc#===` is a special case, that's quite useful
in [case expressions](http://batsov.com/articles/2013/09/24/lambdas-slash-procs-in-case-expressions/),
but should never the used directly.

Of the three general purpose `Proc` methods that are available (it's
actually just one method with two aliases) I'd strongly encourage you
to stick with`Proc#call`. The reasons are quite simple:

* `lambda[arg]` looks like an index access on some data structure and you'd certainly
have to analyze the code context to understand what's going on (especially since the `lambda` is unlikely to actually be named
`lambda` in actual code :-)).

* `lambda.(arg)` is a cute syntactic trick, but it's really easy to overlook the `.` and assume that this is a normal
method call (which probably was the point when this syntax was introduced). `lambda`s in Ruby are not real lambdas (they are instances of the `Proc` class) and we should simply embrace this fact instead of trying to hide it behind awkward syntax.

I value code clarity and readability immensely and I'm not particularly fond of excessive usage of
operator overloading. The use of operators for lambda invocations in Ruby represents the ugly side of operator overloading -
instead of increasing the readability of the code, the operators actually decrease it.
