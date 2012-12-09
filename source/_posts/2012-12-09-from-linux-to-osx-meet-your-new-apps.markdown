---
layout: post
title: "From Linux to OSX: Meet Your New Apps"
date: 2012-12-09 11:41
comments: true
categories: 
- Linux
- OSX
---

## Prelude

It's time I resume what I started in
[my previous article documenting my first year as an OSX user](http://batsov.com/articles/2012/09/09/from-linux-to-osx-1-year-later/)
a few months ago.

In this article I'll focus primarily on the applications I've adopted
during my short time being a Mac OSX user, after being a GNU/Linux
user for quite some time before that. The focus of the article will be
mostly desktop applications, since the command-line tools are more or
less the same in both operating system. I will mention a couple of OSX
specific command-line tools near the end of the article though.

<!--more-->

## Productivity

### Office Suite

On Linux I was mostly using LibreOffice (chiefly its Impress
module) and while it did get the job done I wasn't particularly
fond of it. At some point I was so frustrated with LibreOffice, that I
started running Microsoft Office with
[CodeWeavers CrossOver for Linux](http://www.codeweavers.com/products/). If
you like LibreOffice - it's available on OSX as well. If you don't
like it - you have some solid alternative available.

First, there is a native port of Microsoft Office for OSX. It's a far
cry from the Windows version of the app, but it does have a few
advantages over LibreOffice. If you're doing a lot of document
authoring and editing it might be a good option for you.

The other office suite you might want to explore is Apple's own
**iWorks**. It has a few distinct advantages over Microsoft Office -
you can buy only the apps you need (as opposed to the whole suite), it
integrates great with the OS (but that's hardly a suprise) and it's
much cheaper. I only bought **Pages** (Apple's **Word** alternative)
and **Keynote** (**PowerPoint** alternative). Pages is a so-so
application, but Keynote is simply fantastic. I write a lot of
presentations and for the first I actually enjoy the process.

### Instant Messaging

#### Skype

Skype has a native client for OSX, that's much more stable and
featureful than the Linux one.

#### Pidgin/Kopete

OSX Mountain Lion ships with an app similar to Pidgin and Kopete
called **Messages** (and iMessage in older OSX versions). It supports
a plethora of chat protocols, but it kept constantly disconnecting and
crashing for me, so I started looking for an
alternative. [Adium](http://adium.im/) is a great free IM app that
supports many protocols and works flawlessly (at least for me), so I'd
recommend it to everyone.

#### IRC

If you're in the market for an XChat replacement look no further than
[Colloquy](http://colloquy.info/). Personally I used Emacs's ERC under
Linux and continue to use it under OSX as well.

#### Twitter

Twitter has an official desktop app for OSX, that's available for free
in the Mac App store. It has one notable shortcoming - no retina
support. Rumour has it Twitter will kill the app in the future, but it
gets the job done for the time being and there are plenty of
alternatives lying around.

### Browser

The default OSX browser Safari is great and has some fairly unique
features like pinch to zoom gesture support (smartphone users will
appreciate those). Unfortunately it has a pretty small selection of
plugins and might not be well suited for power users. I recommend the
use of Google Chrome on OSX, since Firefox really seems to lag in terms
of features there (the upcoming Firefox 18 will be the first with
Retina support).

### Email

OSX's default application **Mail** is decent, but nothing
more. Thunderbird is available for OSX, but I personally think it's no
better than Mail. My desktop email client of choice is the delightful
[Sparrow](http://www.sparrowmailapp.com/mac.php). It's the first
desktop email client I ever liked (I used to check my email with
terminal clients and Emacs afterwards) and has great integration with
GMail (it even supports GMail's keyboard shortcuts), Dropbox,
Facebook, etc. While it's a doomed product since
[Google acquired Sparrow](http://www.sparrowmailapp.com/) I plan to
continue using it in the foreseeable future.

### Keyboard remapping

By default you cannot remap that many things in OSX. The small utility
[KeyRemap4MacBook](http://pqrs.org/macosx/keyremap4macbook/) allows
you to do much crazier remappings and despite its name the tool works
on all recent Macs.

### Virtualization Software

The go-to desktop virtualization solution favoured by most Linux users
is VirtualBox and it's available for OSX as well. VirtualBox gets the
job done, but doesn't even come close to
[Parallels](http://www.parallels.com/) in terms of performance,
stability and integration with OSX. Parallels support for Windows
guests is particularly good.

## Software Development

### Text Editing

Every major text editor has a port for OSX, so things are pretty
much the same here. On OSX you'll also get access to
[TextMate](http://macromates.com/). My affection for Emacs is widely
known though. Excellent Emacs builds are available
[here](http://emacsformacosx.com/) and the upcoming Emacs 24.3 will
finally feature OSX Lion style full-screen support. If the mention of
Emacs and vim scares you I'd recommend trying out
[Sublime Text 2](http://www.sublimetext.com/2).

### IDEs

Eclipse, NetBeans and IntelliJ are available (no suprise since they
are all Java apps) and look and perform great on OSX. There's also
Apple's own XCode, which I found unwieldy.

### Terminal Emulator

OSX comes with a pretty barebone terminal emulator called
**Terminal**. I wouldn't advice anyone to spent much time with it.

Install [iTerm2](http://www.iterm2.com/#/section/home). It redefines
the meaning of insanely great.

### Shells

OSX comes with Bash enabled by default, but Zsh is also preinstalled
and you can easily enable it by typing:

``` bash
$ chsh -s /bin/zsh
```

## Media

### Video player

As in Linux [VLC](http://www.videolan.org/vlc/index.html) is the king.

### Audio player

iTunes fits the bill for a basic music player. I still haven't found an
OSX app which I like as much as Linux's Amarok and Exaile.

### UPnP server

Under Linux I used to use MediaTomb and it performed great. It's
available for OSX as well, but was causing a lot of problems for me,
so I finally decided to go with a commercial solution. I heartily
recommend [Playback](http://www.yazsoft.com/products/playback/). Of
course if your media player supports NFS you should go with it instead
of UPnP.

## File Transfer

### FTP

[Filezilla](http://filezilla-project.org/download.php?type=client) is
extremely popular under Linux and has a native OSX version as
well. [Cyberduck](http://cyberduck.ch/) seems to be the top choice of
OSX users.

### Bittorrent

There are plenty of great Bittorrent clients on Linux - Deluge,
KTorrent, Transmission, etc. Transmission is the only with an OSX port
and it seems that it's also the only popular OSX torrent client.

## Package Management

OSX has no official package managent tool but it has plenty of
unofficial ones. Currently
[homebrew](http://mxcl.github.com/homebrew/) seems to be the most
popular option. Its package selection is quite vast and I've rarely
experienced problems with it. While regular users are unlikely to use
anything from outside the Mac App store, developers and power users
should definitely check homebrew out.

## Command Line

Most of the command line applications that you know and love from
Linux are available in OSX (by default or installable via homebrew) as
well (but might be slightly different since Linux ships with GNU's
version of many tools and OSX with BSD's). Here's a few notable OSX
specific commands:

* `open` - opens a file or directory in the appropriate desktop application

``` bash
$ open doc.pdf
```

* `pbcopy` and `pbpaste` allow you to interact with OSX's clipboard

* `launchctl` is a rough equivalent to the `service` and `chkconfig` commands on some Linux distros

* `fs_usage` allows you to monitor your filesystem usage statistics

* `system_profiler` gives you information about your hardware configuration (kind of like `lshw`)

## Epilogue

This was a whirlwind tour of so many apps. I hope that my superficial
treatment of many of them won't stop you from trying them out. It
seems to me that the app selection catalogue on OSX is not as vast as
the one on Linux, but there's also a tendency that established OSX
apps are much more polished and reliable.

