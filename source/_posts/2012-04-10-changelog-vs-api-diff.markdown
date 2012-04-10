---
layout: post
title: "Changelog vs API diff"
date: 2012-04-07 12:22
comments: true
author: Alexander Todorov
categories:
- Linux
- Software
---

*This is a guest post from my friend [Alexander Todorov](http://about.me/atodorov)
who is a QA guru, software engineer and cloud enthusiast!*



**Software changes fast! Open source software even faster!**

And once you start to update dependencies, libraries and frameworks it never ends...
After all the testing and validation you may have done there is no
guarantee that the software will keep working afterwards. 
This is no big deal for small and medium sized projects but becomes a full-time
job for larger projects with longer life span which require constant maintenance
and enhancements. I've seen this time and time again during my work on various projects.
Even a simple *Drupal* based website pops up an update every couple of weeks.


OTOH back porting fixes and keeping stable APIs can be a big business. This is what
*Red Hat* is doing for their *Red Hat Enterprise Linux* distribution. Nearly all changes
are backwards compatible and and the software stack remains stable compared
to upstream *Fedora* or the more upstream projects which comprise it.

Let me say that I don't like to upgrade. Long ago I was using *Debian* **stable**
on my computer. Now I use *RHEL*. No fancy features, no bells and
whistles and more important predictable behavior wrt updates and APIs.
The same approach I take when developing software. I stay away from the latest and
greatest technology simply because it changes too often. I prefer mature frameworks and 
packages which produce new versions every six months or less frequent.
This approach allows me to concentrate on writing code and getting the project done
instead of plumbing bugs introduced by the latest *package foo* version.


All this said I have a very careful approach to upgrades, especially if I'm
using an upstream package. I will first look at the changelog if any. Luckily
many of the mature projects provide comprehensive changelog records. This is
especially true for Perl packages. I'm looking for notices about backward
incompatible changes, API breakage, security notices, major bug fixes,
changes in behavior and the like.
When changelog is not available there's the commit log. I admit this is
not something I usually look at but it happens once in a while. I do this for projects
I'm particularly interested in or otherwise following.
Doing a content diff is another possibility which usually helps you
spot (if you look carefully) some API changes as well. I resort to this if I'm not able to find the upstream
source repository or when it is hosted on something ancient like CVS.


Based on all of this I decide to upgrade or not. With careful planning
of updates (which version, which moment of time) and testing I manage to
minimize the hassle of breaking my projects and spending days fixing
bugs afterwards. Instead I use the time to write some code that kicks ass
(or at least I hope so).


I'm curious to know what sort of information folks do prefer to have
when considering an update? Changelog vs. API diff or seething else? 
I personally prefer well written Changelog and full list of fixed bugs.
Please cast your vote in the comments or visit the 
[survey](http://www.surveymonkey.com/s/T7YW2MJ)! Thank you!
