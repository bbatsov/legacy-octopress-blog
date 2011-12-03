---
layout: post
title: "Solarized for Emacs"
date: 2011-12-03 14:44
comments: true
categories:
- Emacs
---

I've created a new port of the
[Solarized color theme](http://ethanschoonover.com/solarized) for
Emacs 24. While there is
[another existing port of the theme](https://github.com/sellout/emacs-color-theme-solarized)
I've decided to into a separate direction since I've wanted to keep
the development of Solarized and
[Zenburn](https://github.com/bbatsov/zenburn-emacs) for Emacs in sync.

So without further ado here's a screenshot of the theme (or the dark
variant to be precise):

{% img /images/articles/solarized-emacs.png %}

Note that this is a very early version and I haven't fine tuned all
the colors yet. The source code and installation instructions can be
found on [GitHub](https://github.com/bbatsov/solarized-emacs).

The theme is already bundled in
[Emacs Prelude](https://github.com/bbatsov/emacs-prelude) and I'll
submit it to Marmalade soon. Note that I've dropped some things like
the degraded palette and the 16 color palette (at least for now),
since I doubt many people need them. On the other hand - you'll proper
coloring in most prominent modes out of the box.

Feedback, suggestions and patches are always welcome.
