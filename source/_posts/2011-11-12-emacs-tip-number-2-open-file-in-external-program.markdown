---
layout: post
title: "Emacs Tip #2: Open File in External Program"
date: 2011-11-12 11:16
comments: true
categories:
- Emacs
---

Sometimes it's useful to be able to open the file you're editing in
Emacs in an external program. For instance - you might be editing
some HTML file and you might want to see how is it looking in a
browser. I use the following handy command to do so:

``` cl
(defun prelude-open-with ()
  "Simple function that allows us to open the underlying
file of a buffer in an external program."
  (interactive)
  (when buffer-file-name
    (shell-command (concat
                    (if (eq system-type 'darwin)
                        "open"
                      (read-shell-command "Open current file with: "))
                    " "
                    buffer-file-name))))
```

On OSX it would use the `open` program to decide which program to open
the file with, otherwise you'd be prompted to enter the name of the
program in the minibuffer.

I find it convenient to bind the command to `C-c o`:

``` cl
(global-set-key (kbd "C-c o") 'prelude-open-with)
```

This command is naturally part of [Emacs Prelude](https://github.com/bbatsov/prelude).
