---
layout: post
title: "drop-nth in Clojure"
date: 2013-01-20 15:31
comments: true
categories:
- Clojure
---

For some reason the standard Clojure library doesn't have a `drop-nth`
function (although it has `take-nth`). Luckily implementing it is trivial:

``` clojure
(defn drop-nth
  [n coll]
  (->> coll
       (map vector (iterate inc 1))
       (remove #(zero? (mod (first %) n)))
       (map second)))
```

Let's try it out:

``` clojure
(drop-nth 3 (range 1 10))
;; => (1 2 4 5 7 8)
(drop-nth 5 (range 1 10))
;; => (1 2 3 4 6 7 8 9)
(drop-nth 5 (range 1 20))
;; => (1 2 3 4 6 7 8 9 11 12 13 14 16 17 18 19)
```

Looks good to me. Hopefully it will be of some use to someone.
