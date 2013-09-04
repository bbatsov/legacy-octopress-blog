---
layout: post
title: "A couple of useful extensions to Ruby's Enumerable module"
date: 2013-09-03 15:20
comments: true
categories:
- Ruby
---

Ruby's [Enumerable](http://ruby-doc.org/core-2.0.0/Enumerable.html)
module is pretty extensive, but from time to time I wish it had some
extra methods, that are available in
the standard libraries of other languages like Scala, Groovy, Haskell
and Clojure. I'm pretty sure I'm not the only one, that's why I'm writing this post.

Here I'll show you a couple of (hopefully) useful extensions I
implemented for `Enumerable` in the
[Powerpack](https://github.com/bbatsov/powerpack) library. Let's start
with `drop_last` and `take_last`:

``` ruby
(1..10).drop_last(7) #=> [1, 2, 3]
(1..10).take_last(3) #=> [8, 9, 10]
```

Pretty neat! Concise and memory efficient (compared to using
`reverse`). `drop_last` and `take_last` were borrowed from Clojure and
I use them quite often. There are also `drop_last_while` and
`take_last_while`:

``` ruby
[1, 2, 3].drop_last_while(&:odd?) #=> [1, 2]
[1, 2, 3, 5].take_last_while(&:odd?) #=> [3, 5]
```

Summing a collection is also something that pops quite often in the wild:

``` ruby
(1..3).sum #=> 6
[[1,2], [3]].sum #=> [1, 2, 3]
[].sum #=> nil
[].sum(0) #=> 0
```

While I understand why it doesn't make sense to have this in
`Enumerable` by default (not every enumerable can be summed), this method is still
pretty useful and I like having it around.

`Enumerable#one?` is a neat (if somewhat unknown) method that lets
you quickly check if only a single element matches a predicate or a
collection has only one element that's not logically false:

``` ruby
[1, 2, 3].one?(&:even?) #=> true
[1, 2, 4, 5].one?(&:even?) #=> false
[nil, false, 5].one? #=> true
[nil, 1, 2].one? #=> false
```

Unfortunately there is no method `Enumerable#several?`, so I added one to Powerpack:

``` ruby
[1, 2, 3].several?(&:even?) #=> false
[1, 2, 4, 5].several?(&:even?) #=> true
[nil, false, 5].several? #=> false
[nil, 1, 2].several? #=> true
```

Finally, counting the frequencies of elements in a collection is a common enough task to justify having it as method:

``` ruby
[1, :symbol, 'string', 3, :symbol, 1].frequencies
    #     #=> { 1 => 2, :symbol => 2, 'string' => 1, 3 => 1 }
```

None of these methods are spectacular, but I feel they can make the
code we write a little bit more concise, efficient and readable.
Hopefully some of these methods will make it
one day to Ruby proper, but until then you can use them from
[Powerpack](https://github.com/bbatsov/powerpack).

And that's all for today!

I'd really love to hear what methods would you like to add to
`Enumerable` (and other core Ruby modules and classes), so please
share this with me in the comments or on
[Twitter](http://twitter.com/bbatsov). Maybe some of them will land in Powerpack!
