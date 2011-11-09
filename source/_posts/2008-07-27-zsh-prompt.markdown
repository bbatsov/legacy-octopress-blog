---
layout: post
title: "A nice zsh prompt"
categories:
- Z Shell
- Linux
---

Recently I switched to zsh, after being a bash user for almost 5
years. I was in love with everything in zsh from day one, except one
thing – the default prompt. Although zsh ships with several prompt
themes, I didn’t like any of them so I looked around a little bit and
constructed my own humble prompt. Here it goes:

`PROMPT='[%n@%m %~]$ '`

In case you’re wondering what this gibberish means:

%n stands for your username(e.g. bozhidar)

%m stands for the first part of your machine’s hostname(you can use %M
 for the fully qualified name)

%~ stands for the current directory path with your home dir aliased
 with an ‘~’ (if you want to see the path in its natural form use %d
 instead)

All of this strange looking character combinations are called “escape
sequences” and they have special significance to zsh. The rest of the
characters in the prompt definition are represented literally in the
resulting prompt. It looks like this(on my machine):

`[bozhidar@drow ~/store]$`

If you like it simply put the prompt definition like in your .zshrc
file. You may want to put a little bit different version of the prompt
in the root user’s .zshrc(if you use root at all that is):

`PROMPT='[%n@%m %~]# '`

This follows the well established pattern that a normal shell and a
root shell should be easily distinguished visually.
