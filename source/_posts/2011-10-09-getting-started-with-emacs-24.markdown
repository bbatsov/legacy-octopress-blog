---
layout: post
title: "Getting started with Emacs 24"
categories:
- Emacs
---

## Prelude

Last month I've blogged about the
[exciting things are coming up in Emacs 24](/articles/2011/08/19/a-peek-at-emacs24/). What
I failed to mention originally is that altough Emacs 24 is slated for
a Spring 2012 (tentatively) release there is no real reason not to start using it
now. You should also keep in mind that it's feature complete since it
officially entered the feature freeze of its development cycle in July 2011.

I've been using Emacs 24 for several months now and it has been
nothing but rock solid. I guess the only real obstacle currently is
that the way to obtain Emacs 24 is not particularly straightfoward/clear,
hence this post.

I'll discuss here the installation and initial configuration of Emacs
24 on OSX, GNU/Linux and Windows.

<!--more-->

## Installing Emacs 24

#### OS X

Obtaining Emacs 24 on OS X is really simple. There are two popular
ways to do it. The first is to simply download a pretest (or a nightly
build) from [Emacs for OSX](http://emacsformacosx.com). My personal
recommendation would be to get the latest pretest (which is ironically
the first pretest as well) from
[here](http://emacsformacosx.com/emacs-builds/Emacs-pretest-24.0.90-universal-10.6.7.dmg).

That was really easy, right?

The second easy way to obtain Emacs 24 is via
[homebrew](http://mxcl.github.com/homebrew/). Just type the following
incantation in your shell and you're done:

``` bash
$ brew install emacs --cocoa --use-git-head --HEAD
$ cp -r /usr/local/Cellar/emacs/HEAD/Emacs.app /Applications/
```

The second step is optional, but it's recommended if you like to start
Emacs from the launchpad or from Spotlight. Personally I prefer to
start Emacs in daemon mode (`emacs --daemon`), so that I could share a
single Emacs instance between several Emacs clients (`emacsclient
-c/t`).

That's all folk! You may now proceed to the configuration section.

#### Linux

Given that Linux is more or less the home os of Emacs it presents us
with the most installation options. Of course, we can build Emacs from
[source](https://github.com/emacsmirror/emacs) on every distribution
out there, but I rarely bother to do so. Using the distribution's
package manager is a better idea for many reasons - you don't need to
install a build chain and lots of dev libraries, you get updated
versions when they are released and you get automated dependency
manager, just to name a few.

That said, few distributions include in their primary repositories
builds of Emacs 24. Luckily there are some unofficial repos that come
to the rescue.

Debian/Ubuntu users should look no further than the amazing
[emacs-snapshot APT repo](http://emacs.naquadah.org/). You'll find
installation instructions there for all the relevant Debian and Ubuntu
versions out there. High quality, highly recommended builds!

Gentoo users have even less to do, since Emacs 24 can be obtained via
the `emacs-vcs` package in portage, as noted in the official
[Emacs on Gentoo page](http://www.gentoo.org/proj/en/lisp/emacs/emacs.xml).

Unfortunately I wasn't able to find prebuilt Emacs 24 packages for any
of the RPM distros (Fedora, SUSE, Mandriva, etc). Since, I'm Debian
user I have to admit that I didn't look that far, but the source
installation is not particularly hard and is always an option.

#### Windows

There are several ways to obtain precompiled Emacs 24 binaries if
you're a Windows users. The most popular are
[EmacsW32](http://ourcomments.org/cgi-bin/emacsw32-dl-latest.pl),
[Emacs for Windows](http://code.google.com/p/emacs-for-windows/) and
of course the official
[Emacs Windows builds](http://alpha.gnu.org/gnu/emacs/windows/). I've
,personally, never used any builds other than the official ones. The
unofficial builds usually include installers and various patches that
might be of use to some users.

Since I rarely use Windows I cannot give you any more advice on the
choice of a binary vendor.

## Initial configuration

Installing Emacs has always been the easy part, configuring it
properly - not that much. That's why I've created the
[Emacs Prelude](https://github.com/bbatsov/prelude) - an
advanced Emacs setup specifically for Emacs 24 that has been tested to
properly work on OSX, Linux and Windows.

Its installation is dead simple:

``` bash
$ git clone git://github.com/bbatsov/prelude.git path/to/local/repo
$ ln -s path/to/local/repo ~/.emacs.d
```

For Windows Vista/7 the ~(home) folder is
`C:\Users\<USER>\AppData\Roaming\`.

The configuration in the Prelude is commented extensively and will be
improved more along the way. Reading it will be an enlightening
experience for all new Emacs users.

The Prelude itself is a moving target. I've created it recently and I
plan to add a lot more cool things very soon, so stay tuned. If you
have any problems with it or have feature suggestions - do not
hesitate to open tickets and send pull requests.

## Epilogue

Now that I've shown you how easy it is to get a hold of Emacs 24 and
I've provided you with a starting configuration there is really no
excuse not to switch to Emacs 24. Install it, use it, love it!
