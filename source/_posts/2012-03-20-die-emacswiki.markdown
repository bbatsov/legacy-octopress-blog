---
layout: post
title: "Die EmacsWiki, Die!"
date: 2012-03-20 14:49
comments: true
categories: 
- Emacs
- Rant
---

## Prelude

Emacs is slowly, but firmly moving in the right direction with
[Emacs 24](http://batsov.com/articles/2011/08/19/a-peek-at-emacs24/). A
lot of new important features are coming, the release date is nearing,
but there is something worrisome on the otherwise bright Emacs
horizon. It's a remnant from the **Dark Emacs Days** and it's called
[EmacsWiki](http://emacswiki.org).

Shortly put - _EmacsWiki is a blight_. 

<!--more-->

## A Little Bit of Background

Here's the longer story. EmacsWiki was created by
[Alex Schroeder](http://www.emacswiki.org/alex/) (aka **kensanata**)
way back (in 2001) with the goal to become the home of all the Emacs
information one would ever need (both about Emacs in general and its
extensions). I have to admit that this was a noble goal and I know that
Alex had all the right intentions, but unfortunately right intentions
rarely are enough for things to always move in the right
direction. 

The software behind the wiki is called
[OddMuse](http://www.oddmuse.org/cgi-bin/oddmuse) and it's authored by
Alex himself. It's pretty basic Perl script and doesn't feature db
support. Its motto is _No MySQL; no PostgreSQL; no worries._ - wish it
were true...

## The Problems

The EmacsWiki has several epic problems. Here we go:

### Odd Choice for a Wiki

Even if in the beginning OddMuse might have been a good choice (Alex
authored it and MediaWiki didn't exist back then), it hasn't been a
good choice for quite a while. There are much better solutions in
terms of markup support (Markdown anyone?), usability and
performance. Some of the features of the wiki are simply abhorring -
like the lack of user access control; anyone can enter any user name and
edit the wiki... Yep, this is not a joke...

### Moderators, Where Art Though?

I've never seen so much junk in a wiki in my entire life (and I've
seen the wikis of 15-year enterprise systems). When I was
an Emacs beginner I often consulted the wiki for advice - even then I
noticed that there were some suspicious practices being suggested
there. Now I can say with certainly that much of the content there is
total bullshit - it's mostly written by people with very little
knowledge of Emacs (not to mention good Emacs practices). The articles
are littered with crappy advice confusing beginners, have little
structure and are filled with ridiculous questions (questions in an
wiki???). All of this would have been avoided had the EmacsWiki had a
team of moderators to keep shitty contributions at bay. Alas, such a
team does not exist (or does a very crappy job of it).

### Software Distribution Medium

As crazy as it seems a lot of people are using the wiki as a software
distribution mechanism. Instead of hosting their projects in version
control (say [GitHub](http://github.com)) they develop stuff locally,
upload them to the wiki and say that this is the canonical way to
obtain their software. Needless to say - this is a horrible, horrible
practice. I've often encountered on the wiki source files authored by
someone, then edited by 10 different guys, that have a tendency to add
their names to the copyrights sections instead of thinking how their
poor users will understand what exactly was changed in these
files. Sometimes the authors themselves are to blame (for being
fucking lazy), but often someone just copies a snapshot of a project
from version control and uploads it to the wiki, creating problems of
epic proportions for the maintainers, who start receiving bugs about
stuff they never developed in the first place.

For the love of God - take your project(s) to GitHub and develop them
there with pleasure, under the scrutiny of an active and passionate
developer community. Wikis should be used for documentation only!

Tools like audo-install (an extension that supports installing
software from EmacsWiki) should never have existed. el-get should not
have added support for the installation of stuff from the wiki. As
long as such practices are tolerated they will not stop.

Need I remind you that we're now living in the era of
[package.el](http://batsov.com/articles/2012/02/19/package-management-in-emacs-the-good-the-bad-and-the-ugly/)
and distributed version control (Git, Mercurial, Bazaar)? Act accordingly! 

### Jack of All Trades

Documenting each and every Emacs project is an impossible task. And it
should not be centralized. Each project should be responsible for
producing its own up-to-date easy-to-follow crystal-clear
documentation. By putting everything in one place you're just making
sure you'll end up with a pile of out-of-date confusing unstructured
ramblings (the EmacsWiki proves my point).

An EmacsWiki shouldn't list tips on the use of external projects -
such tips should be in the project's wiki. An EmacsWiki should
document the core Emacs experience and customizations only.

## The Solution

Kill the EmacsWiki! (may it be reborn from its ashes)

### Action Plan for The Maintainers

Drop the current format of the wiki - use something standard like
MediaWiki instead of OddMuse. Drop all the articles about Emacs
extensions. Drop all the extensions hosted there. Assemble
a team of moderators. Accept only articles about general Emacs usage
and Emacs Lisp programming.

### Action Plan for Emacs Extensions Authors

If you've got a normal project hosted on GitHub (or a similar service)
- delete everything about your project on the wiki and don't respond
to any bug requests regarding modified copies of your sources
distributed via EmacsWiki.

If you've got a project hosted on the EmacsWiki - there is still
a chance for you to redeem yourself. Migrate your project(s) to GitHub
(you'll thank me later for that). Use their version control, their
issue tracker, their wiki system. Start distributing your project via
Marmalade or MELPA (`package.el` repos). Your life will become much nicer and
the visibility of your project and the possibility to attract new
developers will be significantly boosted. GitHub is a project hosting
solution, the EmacsWiki is not.

### The Regular Users

Boycott the wiki (unless the maintainers take actions)! Submit
documentation only to the official project pages. Ignore projects
hosted on the EmacsWiki. (or migrate them to GitHub if they seem
orphaned and try to rekindle them)

## Epilogue

Do we need an EmacsWiki? Certainly we do! But we need a **real**
EmacsWiki and not this abomination that is currently a detriment to
new Emacs users, instead of help. The wiki needs restructuring, but
first it needs to die. I hope you'll see the truth in my words and
take action instead of commenting how outrageous my claims are. Do
something meaningful for a change - save a project from the EmacsWiki,
contribute documentation to an official project's wiki, package
something on Marmalade...

Die, Die EmacsWiki! I'll be seeing you in hell...
