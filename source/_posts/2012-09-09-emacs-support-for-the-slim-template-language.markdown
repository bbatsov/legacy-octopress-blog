---
layout: post
title: "Emacs Support for the Slim Template Language"
date: 2012-09-09 20:16
comments: true
categories: 
- Emacs
- Rails
---

I'm mostly a Ruby on Rails developer these days and as such I'm pretty
fond of the [Slim template language](http://slim-lang.com). I've
always hated HTML + ERB, since that evil duo encourages all sorts of
ever practices and recently I've adopted Slim as a replacement for
my long time favourite ERB alternative - [Haml](http://haml-lang.com).

I won't discuss here the shortcomings of Haml vs Slim, but I'll share
with you the big advantage Haml has over Slim (for Emacs users at
least) - it has a pretty nice major editing mode for Emacs. Slim's
Emacs support on the other hand is rather iffy and is presently mostly
based on `haml-mode`. That will hopefully change soon, since recently
I've become a co-maintainer of
[slim-mode](http://github.com/minad/emacs-slim) and I plan to improve
it as much as I can (currently I'm mostly working on precise
font-locking). Any help from interested parties is, naturally, most
welcome. I very much doubt that me and
[Daniel Mendler](https://github.com/minad) are the only two people
dreaming of great Slim experience in Emacs. :-)

Let us together eliminate that big Haml advantage. :-)
