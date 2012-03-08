---
layout: post
title: "Emacs Tip #4: Repeat Last Command"
date: 2012-03-08 15:09
comments: true
categories:
- Emacs
- Tip
---

Some times you'd want to quickly repeat an Emacs command several times and
most of the time it won't have a convenient keybinding you can use to
do this. Enter `C-x z` (`repeat`) - it simply repeats the most
recently executed command. And the best part? After you've pressed
`C-x z` once you can continue repeating the last command simply by
pressing `z`. Vi(m) users will probably note that this is quite similar
to the `.` command there.

For instance - if you want to execute the `er/expand-region` command
(part of the
[expand-region package](https://github.com/magnars/expand-region.el))
a few times you can do it like this:

```
M-x er/expand-region
C-x z
z
z
z
```

Neat, ah?
