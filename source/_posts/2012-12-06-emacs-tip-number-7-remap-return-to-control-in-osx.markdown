---
layout: post
title: "Emacs Tip #7: Remap Return to Control in OSX"
date: 2012-12-06 16:06
comments: true
categories: 
- tip
- Emacs
---

One of the major problems when using
[Emacs on OSX](http://batsov.com/articles/2012/10/14/emacs-on-osx/) is
not related to OSX itself - the problem has to do with the Mac's
hardware. Recent Mac keyboards(both laptop and desktop, with the
exception of the wired full size Mac keyboard) lack a right `Control`
key and it happens to be extremely important if you're looking to
fully leverage the power of Emacs.

The traditional solution to the problem is to use a tool like
[KeyRemap4MacBook](http://pqrs.org/macosx/keyremap4macbook/) to remap
the right `Option` key to right `Control` and to use a snippet like
this to make `Command` behave like `Meta` in Emacs:

``` cl
(setq mac-command-modifier 'meta)
```

This works, but it's hardly ideal since you're remapping `Option` at
fairly low level and you won't be able to use it anywhere as `Option`.

A much better idea would be to leverage a little know capability of
KeyRemap4MacBook (a great program which despite its name works with
desktop Macs as well) and map the `Return` key to `Control` only
when it's held down (it will behave like a normal Return key in all
other situations). The option you'll have to find in KeyRemap4MacBook
is in the `Change Return` section and it labeled `Return to Control_R
(+ When you type Return only, send Return)`.

This approach has several advantages.  First and foremost you're not
sacrificing a valuable key like `Option`. Second - it's much easier to
hit `Return` with your right pinky than it is to hit `Option`
(especially if you're using a US layout keyboard - these have long
single row `Return` keys, compared to the short 2 row Returns found on
European keyboards). Lastly, if you've already remapped `CapsLock` to
`Control` (like so many people do) you're getting a pretty symmetrical
mapping on the opposite side of your keyboard.

All in all - remapping `Return` to `Control` is a huge win if you're
using heavily one of Apple's smaller keyboards. Of course, if you have
the option to use an external keyboard you'd do yourself a solid if you
obtained a good full size keyboard like the
[Das Keyboard](http://batsov.com/articles/2008/06/16/das-keyboard/).
