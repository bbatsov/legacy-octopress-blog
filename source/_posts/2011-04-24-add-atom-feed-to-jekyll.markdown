---
layout: post
title: "Add Atom feed to Jekyll powered blog"
categories:
- Jekyll
---

As you know I've recently migrated my blog from WordPress to
Jekyll. One of the things I had to do was add an Atom feed(RSS
sucks). It was quite the easy task. I just had to create an
[atom.xml](https://github.com/bbatsov/blog/blob/master/atom.xml) file
and place in the root of my blog.

Afterwards I only had to link my default layout to the atom feed:

``` xml
<link rel="alternate" type="application/atom+xml" href="atom.xml" title="Atom feed">
```

At this point I was able to subscribe to my new atom feed(and
hopefully my followers(which I may or may not have) were able to do
the same).
