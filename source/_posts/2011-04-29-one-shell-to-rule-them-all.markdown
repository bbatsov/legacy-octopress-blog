---
layout: post
title: "One shell to rule them all..."
categories:
- Z Shell
---

## Prelude

I've been using zsh for about three years now and continue to be
impressed the its immense power and flexibility. Switching from bash
to zsh was a decision as good as switching from Windows to GNU/Linux,
from vim to Emacs, from Eclipse to IntelliJ IDEA. In other words - it
was an extremely good decision. :-)

So I want to finally get the word out, showcase some nice zsh features
and probably persuade a couple of bash users to try it. Be warned,
however - after you try it there is no going back...

## Getting started

Most distros come with bash by default so you'll probably need to
install zsh first and configure it as your user's shell. On Fedora
you'd do:

``` bash
$ sudo yum install zsh
$ chsh -s /bin/zsh
```

The next time you login a terminal wizard with start up asking you
about some basic zsh options that you might want to enable. I suggest
you to enable them all except the beep option. In the end the wizard
will save the new configuration to the file .zshrc in your user's home
folder.

Alternatively you may just use a preconfigured .zshrc, like this one:

``` bash
# Lines configured by zsh-newuser-install
HISTFILE=~/.histfile
HISTSIZE=1000
SAVEHIST=1000
setopt appendhistory autocd extendedglob nomatch notify correct_all
unsetopt beep
bindkey -e
# End of lines configured by zsh-newuser-install
# The following lines were added by compinstall
zstyle :compinstall filename '/home/bozhidar/.zshrc'

autoload -Uz compinit
compinit
# End of lines added by compinstall
```

I don't like very much the default zsh prompt and I generally change
it right away. Have a look at my other
[short article](/Z%20Shell/Linux/2008/07/27/zsh-prompt.html) on the topic.

There a couple of configuration files related to zsh that you should
know about:

* .zshrc - runs for each new shell(roughly equivalent to .bashrc)
* .zprofile - runs only for login shells(like .bash_profile)
* .zlogout - runs on logout
* .zshenv - holds environmental variables

Here's an example .zshenv file:

``` bash
export JAVA_HOME=/usr/java/latest

export SCALA_HOME=/opt/scala-2.8.1.final

export M2_HOME=/opt/apache-maven-3.0.2

export EDITOR="emacsclient -t"
export ALTERNATE_EDITOR=""

#needed to properly display complex color-themes in Emacs and vim
export TERM=xterm-256color

typeset -U path
path=($M2_HOME/bin $SCALA_HOME/bin ~/bin ~/Projects/work/bin $path)
```

Please note the way in which the PATH variable is set in zsh, which
differs substantially from bash(it's just exported there as any other variable).

## Playing around

At this point you have the legendary zsh autocompletion configured and
you have enabled many of the zsh core features.

**autocd** allows you to navigate to folders only with their name
without the cd command. One of my favourite features. Now you can do
things like:

``` bash
[bozhidar@bozhidar ~]$ Downloads
[bozhidar@bozhidar ~/Downloads]$
```

Instead of:

``` bash
[bozhidar@bozhidar ~]$ cd Downloads
[bozhidar@bozhidar ~/Downloads]$
```

By the way autocd was added in bash 4.0 as well. You can enable it there with:

``` bash
[bozhidar@bozhidar ~]$ shopt -s autocd
```

**appendhistory** all your open shells share the same history which is
handy if you want to refer commands from one shell in another with
say Ctrl+R(reverse-history-search)

**extendedglob** allows you to recursive look for files in folders:

``` bash
[bozhidar@bozhidar ~]$ ls somedir/**/Makefile
```

is equivalent to:

``` bash
[bozhidar@bozhidar ~]$ find somedir -name Makefile
```

Most zsh users never use find for simple file look up. This feature
was also added to bash 4.0 but it works in a slightly different
manner.

``` bash
$ shopt -s extglob
```

**correct** - autocorrects mistyped commands

``` bash
[bozhidar@bozhidar]$ cta ~/.zshrc
zsh: correct 'cta' to 'cat' [nyae]?
```

## Keybindings

By default zsh uses Emacs keybindings which is perfect for a long time
Emacs user like me. zsh doesn't use readline, instead it has its own
line editing library called zle, which is much more powerful. vi users
are not forgotten and can switch zsh to vi keybindings with the
command:

``` bash
bindkey -v
```

Mind that by default you'll be in "insert" mode and have to press ESC
to go into command mode.

You can also create custom keybindings like this:

``` bash
bindkey '^[[H' beginning-of-line
bindkey '^[[F' end-of-line
```

This will bind the Home and End keys to the commands beginning-of-line and end-of-line.
## Aliases

Zsh has three different kinds of shell aliases.

**Regular** - same as in bash:

``` bash
alias ll='ls -l'
```

**Suffix** - suffix aliases are supported in zsh since version
4.2.0. Some examples:

``` bash
alias -s tex=emacs
alias -s html=google-chrome
```

Now when you type in the console

``` bash
$ somefile.tex
```

it will be opened automatically with Emacs. Similarly somefile.html
would be opened by google-chrome. As you might imagine this feature is
quite handy.

**Global** - global aliases can be used anywhere in the command line(as
opposed to regular aliases that can used only in the beginning). Example:

``` bash
alias -g ...='../..'
cd ...
```

## Some tips and tricks

* press Alt+q in the middle of a command you're typing. This will clear
the console prompt and allow you execute another command(like a man lookup). Afterwards
the things you've typed before the Alt+q will magically reappear.

* Imagine you're in the folder **project/4.0/module**. Typing:

``` bash
cd 4.0 5.0
```

Will take you to a folder named project/5.0/module(assuming that it exists of course). In general
the command has the format `cd old new`.

* zsh comes with a built-in pager(similar to less). To try it just type <somefilename. This is
  more or less equivalent to typing `less somefilename`.

## Useful resources

* [zsh reference card](http://www.bash2zsh.com/zsh_refcard/refcard.pdf)
* [zsh manual](http://zsh.sourceforge.net/Doc/zsh_a4.pdf)
* ["A User's Guide to Z-Shell"](http://zsh.sourceforge.net/Guide/zshguide.html)
* [zsh wiki](http://zshwiki.org/home/)
* [zsh lovers](http://grml.org/zsh/zsh-lovers.html) - collection of
  tips and tricks
* ["From Bash to Z Shell - Conquering the Command Line"](http://www.bash2zsh.com/)

## Epilogue

There is no easy way to sum up everything that makes zsh great in a single blog post. I'll try to
expand and improve it in time. I hope I've whetted your appetite to try out zsh. If you like it
well enough(of which I'm most certain you should have a look at the resources in the end as well).

