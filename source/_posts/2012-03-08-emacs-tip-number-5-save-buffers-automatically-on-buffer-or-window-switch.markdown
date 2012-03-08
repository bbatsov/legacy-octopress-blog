---
layout: post
title: "Emacs Tip #5: Save Buffers Automatically on Buffer or Window Switch"
date: 2012-03-08 15:58
comments: true
categories:
- Emacs
- Tip
---

When I program in Java I usually leave the comfort of Emacs and use
IntelliJ IDEA instead (for various reasons that are irrelevant to this
post). IDEA has one particularly nice feature - "auto-save on focus
lost". Basically you never have to hit `C-s` there explicitly, because
any time your current editor window loses focus its contents get
flushed to the disk automatically. Implementing something exactly the
same in Emacs is impossible (at least in Emacs Lisp), but we can
create a solution that is similar in spirit at least - we can
auto-save buffers when we switch the Emacs window or the current
buffer (which are more or less the most popular ways to change editing
focus in Emacs). This is easy to achieve in Emacs Lisp:

```cl
;; use shift + arrow keys to switch between visible buffers
(require 'windmove)
(windmove-default-keybindings 'super)

;; automatically save buffers associated with files on buffer switch
;; and on windows switch
(defadvice switch-to-buffer (before save-buffer-now activate)
  (when buffer-file-name (save-buffer)))
(defadvice other-window (before other-window-now activate)
  (when buffer-file-name (save-buffer)))
(defadvice windmove-up (before other-window-now activate)
  (when buffer-file-name (save-buffer)))
(defadvice windmove-down (before other-window-now activate)
  (when buffer-file-name (save-buffer)))
(defadvice windmove-left (before other-window-now activate)
  (when buffer-file-name (save-buffer)))
(defadvice windmove-right (before other-window-now activate)
  (when buffer-file-name (save-buffer)))
```

Obviously this code could have been written in a more compact manner
with the use of a macro, but I've decided to use this more verbose
variant for the sake of simplicity. We assume that you want to
auto-save your current work (buffer) when you switch to a new buffer
or to a new window (with either `C-x o` (`other-window`) or a
`windmove` command).

XEmacs has a hook called `deselect-frame-hook` that can take the
concept even further, but it's absent from GNU Emacs.

So, that's all for this tip, folks! I hope you've enjoyed it!
Personally I find it much more useful that the standard auto-save
mechanism in Emacs. And one more thing -
[Emacs Prelude](https://github.com/bbatsov/emacs-prelude) naturally
enables this functionality by default.
