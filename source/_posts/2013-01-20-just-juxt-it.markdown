---
layout: post
title: "Just juxt it!"
date: 2013-01-20 18:16
comments: true
categories:
- Clojure
---

`juxt` is one remarkably useful core Clojure function, that doesn't
seem to be widely used (or understood for that matter), but is part of
the arsenal of every experienced Clojure hacker.

Looking at the official docs you'll see that `juxt` takes a set of
functions and returns a function that is the juxtaposition of those
functions. The returned function takes a variable number of
arguments, and returns a vector containing the result of applying each
function to the arguments (from left to right). Basically:

``` clojure
((juxt a b c) x) => [(a x) (b x) (c x)]
```

At first glace that probably doesn't seem particularly useful. Let's
see some practical applications of `juxt`. What if we wanted to split
a sequence into two sequences - one with the values that satisfy some
predicate and one with the values that don't. While there are many
ways to do so, `juxt` offers one particularly elegant:

``` clojure
;; illustration of the general idea
((juxt filter remove) pred coll)

;; separate the even from the odd numbers
((juxt filter remove) even? (range 1 10))
;; => [(2 4 6 8) (1 3 5 7 9)]
```

`juxt` is also quite helpful when dealing with multiple map keys:

``` clojure
;; extract the values of a couple of maps keys
((juxt :alias :name) {:alias "Batman" :name "Bruce Wayne"})
;; => ["Batman" "Bruce Wayne"]

;; sort a vector of maps by a composite criteria
(sort-by (juxt :alias :name)
         [{:alias "Batman" :name "Bruce Wayne"}
          {:alias "Robin" :name "Jason Todd"}
          {:alias "Robin" :name "Tim Drake"}
          {:alias "Robin" :name "Dick Grayson"}])

;; => ({:name "Bruce Wayne", :alias "Batman"} {:name "Dick Grayson", :alias "Robin"} {:name "Jason Todd", :alias "Robin"} {:name "Tim Drake", :alias "Robin"})
```

Hopefully this short article has whetted your appetite and you'll find
even more elegant uses for `juxt` in your code.
