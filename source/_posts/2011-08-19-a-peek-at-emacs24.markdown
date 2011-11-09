---
layout: post
title: "A peek at Emacs 24"
categories:
- Emacs
---

## Prelude

Recently I've decided to have a look at the current development
version of Emacs - namely Emacs 24. I was quite impressed with the work done
by the development team so far so I decided to share some of the cool things
I've found in Emacs 24.

It seems to me that this will be the most important Emacs release in
quite some time.

## Installation changes in Emacs 24

There are a couple of new build flags support in Emacs 24 - most
notably there is GTK 3.0 support present. You can enable it by passing
the **--with-x-toolkit=gtk3** flag to _configure_. There is also built-in
support for selinux (that can be disabled at build time) and the
installed info and man pages are now compressed by default.

All in all - nothing major has changed with the installation process.

## General changes

#### Completion improvements

There has been a lot of work done in the completion department. For
instance **shell-mode** now uses pcomplete rules and the standard
completion UI, which is pretty cool IMHO. Some other insteresting
improvements (mostly copied directly from Emacs' NEWS files):

* Many packages have been changed to use _completion-at-point_ rather than
their own completion code.
* Completion in a non-minibuffer now tries to detect the end of completion
and pops down the \*Completions\* buffer accordingly.
* Completion can cycle, depending on completion-cycle-threshold.
* There is a new completion style called _substring_.
* Completion style can be set per-category with _completion-category-overrides_.
* Completion of buffers now uses substring completion by default.
* _completing-read_ can be customized using the new variable
_completing-read-function_.
* _minibuffer-local-filename-must-match-map_ is not used any more.
Instead, the bindings in _minibuffer-local-filename-completion-map_ are combined
with minibuffer-local-must-match-map.

#### Scrolling improvements

Scrolling has always been a sour subject in Emacs. Emacs 24 finally
alleviates many of the long standing issues in the scrolling department:

* New scrolling commands _scroll-up-command_ and _scroll-down-command_
(bound to C-v/[next] and M-v/[prior]) do not signal errors at top/bottom
of buffer at first key-press (instead move to top/bottom of buffer)
when a new variable _scroll-error-top-bottom_ is non-nil.

* New scrolling commands _scroll-up-line_ and _scroll-down-line_
scroll a line instead of full screen.

* New property _scroll-command_ should be set on a command's symbol to
define it as a scroll command affected by _scroll-preserve-screen-position_.

* If you customize _scroll-conservatively_ to a value greater than 100,
Emacs will never recenter point in the window when it scrolls due to
cursor motion commands or commands that move point (e.f., _M-g M-g_).
Previously, you needed to use _most-positive-fixnum_ as the value of
_scroll-conservatively_ to achieve the same effect.

* __Aggressive__ scrolling now honors the scroll margins.
If you customize _scroll-up-aggressively_ or
_scroll-down-aggressively_ and move point off the window, Emacs now
scrolls the window so as to avoid positioning point inside the scroll
margin.

#### GTK improvements

Linux users are in for a treat:

* GTK scroll bars are finally placed on the right by default.
You can still use _set-scroll-bar-mode_ to change this.
* GTK tool bars can have just text, just images or images and text.
Customize _tool-bar-style_ to choose style.  On a Gnome desktop, the default
is taken from the desktop settings.
* GTK tool bars can be placed on the left/right or top/bottom of the frame.
The frame-parameter tool-bar-position controls this.  It takes the values
top, left, right or bottom.  The **Options => Show/Hide** menu has entries
for this.
* The colors for selected text (the region face) are taken from the GTK
theme when Emacs is built with GTK.
* Emacs uses GTK tooltips by default if built with GTK.  You can turn that
off by customizing x-gtk-use-system-tooltips.

#### Cocoa (OS X improvements)

OS X users seem to be a bit neglected, but still:

* the annoying bug with the cursor not having an inverse video face
  (meaning you couldn't see the symbol under it) is finally fixed
* the menu bar can be hidden by customizing
ns-auto-hide-menu-bar.

#### ELPA (a package manager for Emacs)

* An Emacs Lisp package manager (aka ELPA) is now included.
This is a convenient way to download and install additional packages,
from a package repository at elpa.gnu.org.

* The addition of external repositories is also supported ( I'm
  particularly fond of the [Marmalade repo](http://marmalade-repo.org/))

* _M-x list-packages_ shows a list of packages, which can be
selected for installation.

* New command _describe-package_, bound to _C-h P_.

* By default, all installed packages are loaded and activated
automatically when Emacs starts up.  To disable this, set
_package-enable-at-startup_ to nil.  To change which packages are
loaded, customize _package-load-list_.

I'm personally a little bit underwhelmed by ELPA at this point. It
lacks something that I deem rather critical - the ability to upgrade
already installed packages automatically. Hopefully, this deficiency
will be amended in the near future.

There is also the restrictive licensing policy that GNU enforces
that will certainly prevent a lot of packages from being distributed
via the official ELPA repo.

#### Custom color themes

Most hackers are very fond of custom color themes. I'm no exception -
after all I'm the maintainer of the [Zenburn color theme for Emacs](https://github.com/bbatsov/zenburn-emacs). The
problems with custom color themes so far was that depended on the
horrible external package color-theme, that wasn't maintained
particularly actively in the past few years.

Now Emacs 24 comes with a built-in theming infrastructure
affectionately called **deftheme** and several quite nice themes that
Emacs users can choose from (like tango). I've already ported Zenburn to the
deftheme infrastructure, so if you like it be sure to give it a
try. The magic command you'll need to keep in mind is called _load-theme_.

## Editing improvements

Emacs is after all mostly an editor and there is a lot of work done in
the editing area in 24:

#### Search changes

* C-y in Isearch is now bound to isearch-yank-kill, instead of
isearch-yank-line.

* M-y in Isearch is now bound to isearch-yank-pop, instead of
isearch-yank-kill.

* M-s C-e in Isearch is now bound to isearch-yank-line.

#### General
* There is a new command _count-words-region_, which does what you expect.

* _completion-at-point_ now handles tags and semantic completion.

* The default value of _backup-by-copying-when-mismatch_ is now t.

* The command _just-one-space_ (C-SPC), if given a negative argument,
also deletes newlines around point.

#### Deletion changes

* New option _delete-active-region_.
If non-nil, C-d, [delete], and DEL delete the region if it is active
and no prefix argument is given.  If set to _kill_, these commands
kill instead.

* New command _delete-forward-char_, bound to C-d and [delete].
This is meant for interactive use, and obeys _delete-active-region_.
The command _delete-char_ does not obey _delete-active-region_.

* _delete-backward-char_ is now a Lisp function.
Apart from obeying _delete-active-region_, its behavior is unchanged.
However, the byte compiler now warns if it is called from Lisp; you
should use delete-char with a negative argument instead.

* The option _mouse-region-delete-keys_ has been deleted.

#### Selection changes

The default handling of clipboard and primary selections was changed
to conform with modern X applications.  In short, most commands for
killing and yanking text now use the clipboard, while mouse commands
use the primary selection.

In the following, we provide a list of these changes, followed by a
list of steps to get the old behavior back if you prefer that.

* _select-active-regions_ now defaults to t.
Merely selecting text (e.g. with drag-mouse-1) no longer puts it in
the kill ring.  The selected text is put in the primary selection, if
the system possesses a separate primary selection facility (e.g. X).

* _select-active-regions_ also accepts a new value, _only_.
This means to only set the primary selection for temporarily active
regions (usually made by mouse-dragging or shift-selection);
"ordinary" active regions, such as those made with C-SPC followed by
point motion, do not alter the primary selection.

* _mouse-drag-copy-region_ now defaults to nil.

* mouse-2 is now bound to _mouse-yank-primary_.
This pastes from the primary selection, ignoring the kill-ring.
Previously, mouse-2 was bound to _mouse-yank-at-click_.

* _x-select-enable-clipboard_ now defaults to t on all platforms.
* _x-select-enable-primary_ now defaults to nil.
Thus, commands that kill text or copy it to the kill-ring (such as
M-w, C-w, and C-k) also use the clipboard---not the primary selection.

* The "Copy", "Cut", and "Paste" items in the "Edit" menu are now
exactly equivalent to, respectively M-w, C-w, and C-y.

* Note that on MS-Windows, _x-select-enable-clipboard_ was already
non-nil by default, as Windows does not support the primary selection
between applications.

* Support for X cut buffers has been removed.

* Support for X clipboard managers has been added.

* To inhibit use of the clipboard manager, set
_x-select-enable-clipboard-manager_ to nil.

## New modes

* Occur Edit mode applies edits made in \*Occur\* buffers to the
original buffers.  It is bound to C-x C-q in Occur mode. This
basically removes the need for an external package such as iedit.el.

* New global minor modes electric-pair-mode, electric-indent-mode,
and electric-layout-mode. One of my favourite new
additions. electric-pair-mode renders obsolete the popular
autopair-mode and electric-indent-mode and electric-layout-mode
provide a much more IDE feel to the editing experience in Emacs. This
triumvirate of modes has been a long time coming

* secrets.el is an implementation of the Secret Service API, an
interface to password managers like GNOME Keyring or KDE Wallet.  The
Secret Service API requires D-Bus for communication.  The command
_secrets-show-secrets_ offers a buffer with a visualization of the
secrets.

* notifications.el provides an implementation of the Desktop
Notifications API.  It requires D-Bus for communication.

* soap-client.el supports access to SOAP web services from Emacs.
soap-inspect.el is an interactive inspector for SOAP WSDL structures.


## Epilogue

Emacs 24 brings quite a lot to the table. I've barely scratch the
surface as far as the new features are concerned. There is so much
more - improvements to lots of the existing modes (most notably much
better support for distributed VC systems such as Git, Mercurial and
Bazaar), internal cleanups and improvements, etc.

I truly feel that Emacs 24 will be the most important Emacs release in
a long long time and I commend the new dev team leads for their
passion and resolve to modernize Emacs.

Expect future blog posts dedicated to specific new features and
improvements.

P.S. Btw [The Emacs Prelude](https://github.com/bbatsov/emacs-prelude)
already makes use of some the new features from Emacs 24. In due time
it will make use of much more of them. It's one of the very few
advanced Emacs setups targeting exclusively Emacs 24.

**Update**

A lot of people have been asking me about the level of stability and
usability of Emacs 24 at this point since I didn't mention them at my
article. I've been using Emacs 24 for all of my work for about a month
now and I've experienced absolutely no crashes/freezes/any sort of
instabilities. On the usability side I've encountered a few bugs that
might be related to some work in progress (for instance face inheritance doesn't
work with deftheme), but nothing major.

If you're considering trying out Emacs 24 more seriously - my advice
is to go for it. With no clear release date in sight you might be in
for a long wait before the final release is here and you'll be missing
on some really great features in the meantime. I'll write a separate
article soon detailing how to get started with Emacs 24 on the most
popular platforms (Linux, OS X and Windows).
