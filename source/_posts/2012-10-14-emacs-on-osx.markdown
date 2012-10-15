---
layout: post
title: "Emacs on OSX"
date: 2012-10-14 22:03
comments: true
categories: 
- emacs
- osx
---

## Prelude

In this article I'll share with you a few tips and tricks about
running Emacs under the Max OSX operating system.

## Installation

While Emacs is available for installation from
[various sources](http://wikemacs.org/wiki/Installing_Emacs_on_OS_X)
I personally recommend you to use the
[Emacs for Mac OSX binary distribution](http://wikemacs.org/wiki/Installing_Emacs_on_OS_X).

Installation via Homebrew is also a decent option, although it more time consuming.

After the installation you might want to wipe out the ancient Emacs 22
that ships with OSX by default(its presence will only cause headaches, trust me):

``` bash
$ sudo rm /usr/bin/emacs
$ sudo rm -rf /usr/share/emacs
```

Keep in mind that the OSX updates will (unfortunately) bring Emacs 22 back from the dead, so
you might consider altering your `PATH` instead.

Alternatively you can just create an alias in your shell and when you
invoke `emacs` it will run the newly installed version:

``` bash
$ alias emacs="/Applications/Emacs.app/Contents/MacOS/Emacs"
```

If you installed via Homebrew that path might look like this:

``` bash
$ alias emacs="/usr/local/Cellar/emacs/24.2/Emacs.app/Contents/MacOS/Emacs -nw"
```

To make it permanent, if using bash, add that line to
`~/.bash_profile`. zsh users will want to update `~/.zshrc` instead.

## Full-screen support

The Homebrew Emacs formula includes a patch providing the `M-x
ns-toggle-fullscreen` command for switching between normal and
full-screen modes. It works well, but does not provide the typical OS
X Lion full-screen app experience. In particular, it remains on the
desktop, obscuring non-full-screen applications, rather than moving to
its own space. For OSX Lion style fullscreen support have a look at
this
[article](http://sourcematters.org/2012/04/10/full-screen-emacs-24-for-os-x-lion.html).

Another option that you might want to explore is
the [maximizer](http://osxdaily.com/2011/07/22/enable-full-screen-support-all-apps-os-x-lion-maximizer/)
utility that brings full-screen support for all Cocoa apps under Lion.

## Keybindings

I heartily recommend you to remap your *Caps Lock* key to *Control*. This
can be easily done via *Preferences -> Keyboard -> Modifier Keys*. If
you're using a laptop keyboard or the bluetooth keyboard you'll
definitely want to remap your right Option key to Control as
well. No one can use effectively Emacs without a right Control
key. Remapping it is a bit more involved and requires the use of the
third-party utility
[KeyRemap4MacBook](http://pqrs.org/macosx/keyremap4macbook/).

On a regular Mac keyboard you'll probably want to map Command to Meta
and Option to Super. On an external Windows keyboard you'll want to
map Command to Super and Option to Meta (on Windows keyboard the
Command and Option keys are swapped). Add this to your `init.el` (or
`.emacs`) file:

``` cl
(setq mac-command-modifier 'super)
(setq mac-option-modifier 'meta)
```

If you often switch between your laptop keyboard and an external
Windows keyboard (like me) you might want to define this helper
command and bind it to some key combo (`C-c w` in the example):

``` cl
(defun swap-meta-and-super ()
  "Swap the mapping of meta and super. Very useful for people using their Mac
with a Windows external keyboard from time to time."
  (interactive)
  (if (eq mac-command-modifier 'super)
      (progn
        (setq mac-command-modifier 'meta)
        (setq mac-option-modifier 'super)
        (message "Command is now bound to META and Option is bound to SUPER."))
    (progn
      (setq mac-command-modifier 'super)
      (setq mac-option-modifier 'meta)
      (message "Command is now bound to SUPER and Option is bound to META."))))

(global-set-key (kbd "C-c w") 'swap-meta-and-super)
```

## Setting the PATH variable

Long story short - if you're running Emacs from Spotlight (or any
other launcher for that matter) your `PATH` and `exec-path` variables
won't be same as the ones in your shell (and that's every nasty since
you want be able to run some external programs from Emacs). The best
way to handle this would be installing the package
[exec-path-from-shell](https://github.com/purcell/exec-path-from-shell)
by Steve Purcell.

## Flyspell

For flyspell to work correctly you'll need to install aspell plus a few dictionaries.

``` bash
$ brew install aspell --lang=en
```

## More goodies

If you want to spare yourself part of the headache of configuring
Emacs on OSX and get a lot of extra firepower you might want to install
[Emacs Prelude](https://github.com/bbatsov/prelude) - an enhanced
Emacs 24.x configuration (developed by yours truly) that should make
your experience with Emacs both more pleasant and more powerful.
