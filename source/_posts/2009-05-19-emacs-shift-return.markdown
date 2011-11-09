---
layout: post
title: Emulate the behaviour of Return+Shift(insert new line) from popular IDEs(IDEA, Eclipse) in Emacs
categories:
- Emacs
- IntelliJ
---

I’m very fond of the ability to insert a new line below the line I’m
currently at, and to position the cursor at the beginning of that new
line, offered by most IDEs, such as IntelliJ IDEA, Eclipse. It’s
usually bound to Return(Enter)+Shift. Emacs(as far as I know) doesn’t
have a function that does this thing by default, but one can easily
create one, combining several well known functions in the process and
bind that new function to the desired key combination. Here’s the
snippet one might have in his .emacs(or other) “configuration” file:

``` cl
;; insert an empty line after the current line and position the cursor on its beginning
(defun insert-empty-line ()
 (interactive)
 (move-end-of-line nil)
 (open-line 1)
 (next-line 1))

(global-set-key [(shift return)] 'insert-empty-line)
```
