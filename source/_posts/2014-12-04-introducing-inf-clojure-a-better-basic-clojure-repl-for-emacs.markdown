---
layout: post
title: "Introducing Inf-clojure - a Better Basic Clojure REPL for Emacs"
date: 2014-12-04 12:45
comments: true
categories:
- Clojure
- Emacs
---

At [Clojure/conj](http://clojure-conj.org/) I had the chance to shake
Rich Hickey’s hand and exchange a few words with him. When I asked him
whether he currently uses CIDER or Cursive for Clojure development he
replied that he preferred a simpler solution – `clojure-mode` &
`inferior-lisp-mode`. I was a bit surprised because `clojure-mode`’s
integration with `inferior-lisp-mode` sucks (big time). It has always
been extremely limited and was never really improved/extended. It has
no Clojure specific features and no code completion. I felt that Rich
and all the people using inferior-lisp-mode deserved something better,
so I quickly put together [inf-clojure](https://github.com/clojure-emacs/inf-clojure).

`inf-clojure` provides some Clojure specific features like showing a
var’s doc or source, derives some core functionality from `clojure-mode`
and even features basic code-completion (and `company-mode`
support). That’s not much admittedly, but it’s a good start. Extending
`inf-clojure` is super easy and I expect that we’ll add a bit more
features to it along the way (e.g. macroexpansion).

`inf-clojure` is available in MELPA and will eventually replace
completely `inferior-lisp-mode` when `clojure-mode` 4.0 is released.

Keep in mind that `inf-clojure` is nothing like CIDER and will never
be. CIDER will always be the powertool for Clojure programming in
Emacs. I do understand, however, that some people are overwhelmed by
CIDER and some people simply don’t need anything sophisticated. I hope
they’ll enjoy `inf-clojure`!
