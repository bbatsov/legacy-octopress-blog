---
layout: post
title: "Emacs Tip #6: Remove variable &amp; function definitions"
date: 2012-10-20 20:29
comments: true
categories: 
- emacs
- tip
---

From time to time you might want to void (unbind) a variable or a
function definition in Emacs. Most often you'll probably be dealing
with variables created with `defvar` whose values you'll want to
update.  The magic functions you need are the following:

``` cl
;; this will make the symbol my-nasty-variable's value void
(makunbound 'my-nasty-variable)
;; this will make the symbol my-nasty-function's
;; function definition void
(fmakunbound 'my-nasty-function)
```

The names aren't exactly intuitive and even I happen to forget them from time to
time. Now at least I'll now where to look for them if that happens
again. :-)
