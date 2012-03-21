---
layout: post
title: "All Hands on Deck! (or the Action Plan for a new Emacs community wiki)"
date: 2012-03-21 11:11
comments: true
categories: 
- Emacs
---

## Prelude

Yesterday I wrote a highly
[controversial article about the state of the EmacsWiki](http://batsov.com/articles/2012/03/20/die-emacswiki/)
and suggested a few things we can do to make things better. I got the
usual batch of hate mail and some remarks on the poor quality of my
English and writing style (which generally amuse me a lot). But I
got much more encouraging feedback from **a lot** of Emacs community
members. So here our story continues...

<!--more -->

## On The Essence of Things

Some people accused me that I don't even know what I wiki is. To them
I'd like to say that a thing is not its dictionary/encyclopedia
definition. A thing is what it's perceived to be. People expect wiki
entries to look and behave like those found in MediaWiki or Confluence
and not like some mixture of a wiki, forum and irc conversation...

## A Word from Our Sponsor

Alex wrote a
[public response on the EmacsWiki](http://www.emacswiki.org/emacs/2012-03-20)
yesterday, that I'd first like to share (since probably more people
will see it here, than there). I publish it here with no alternations:

{% blockquote Alex Schroeder, Creator and Maintainer of EmacsWiki.org %} 

Bozhidar Batsov is apparently very frustrated with Emacs Wiki. He
seems to think that we should start over – use new software, add
moderators, guidelines, and sorts of fancy stuff. My answer is the
same as it was back in 2008 (http://www.emacswiki.org/emacs/MissionRant).

One of his ideas I actually agree with. "Submit documentation only to
the official project pages." Absolutely. :)

Some ideas I am luke warm about: "package something on Marmalade…"
Sure, why not? I have never used Marmalade, but I encourage you to
improve the tools you use. There's also "don't respond to any bug
requests regarding modified copies of your sources distributed via
EmacsWiki." I also don't want to encourage bug reports on the
wiki. Use the facilities built into Emacs to report bugs. But almost
all of you know that.

But other ideas?

"Drop the current format of the wiki - use something standard like
MediaWiki instead of OddMuse." How is reformatting the pages going to
improve them?

"Drop all the articles about Emacs extensions." Just delete them? Are
you at least going to rewrite them and move them to the appropriate
project pages out there? Or are you just going to delete them? Taking
away and not giving back?

"Drop all the extensions hosted there." Some of the old code has no
other home. Some of the old code is here for the poor sods stuck with
Emacs 20. Are you going to package them for ELPA or Marmalade or
whatever you are going to suggest instead?

Some of you – like Drew Adams – keep their packages on the wiki. For
those packages, I don't see any alternative. Are you going to maintain
his software? Fix his bugs? Develop his features? Unless you are, I
guess you can try and fork his stuff and keep it on whatever other
system you want. But please don't suggest taking something away
without giving something in return.

"Assemble a team of moderators." Indeed. Moderators! Where have you
been hiding for the last ten years! Are you volunteering? I'm a bit
wary regarding your deletionist tendencies. But perhaps you’d like to
start with a new Table of Contents and new top-down menus where only
the pages you personally vetted and checked are listed. That would be
an awesome thing to do! Of course, there’s no need to delete anything
in order for you to do this. Just arrange the stuff you like and do
it.

In fact, in order to do it, just do it.

"Accept only articles about general Emacs usage and Emacs Lisp
programming." How is that going to work – more deleting? I don't
know... I don't think you understand where the value of Emacs Wiki
comes from. Perhaps you should write a book about Emacs? Collect a
team of authors and editors and deletionists, take a copy of the wiki,
and just do it right.

Also, less hyperbole when posting... :P
{% endblockquote %}

Here's my two cents on the letter:

* The markup format hardly matters. A new wiki engine would give us
better structure of the wiki as whole (like separate discussion pages
for one). 

* Dropping it from the wiki doesn't mean we'll delete the code
forever. What I meant was - dump all the extensions to some archive
for the interested parties and remove them from the wiki. You're
basically putting words in my mouth.

* We should care for the bad choices some people made (like Drew - all
my respect to his work). With so many free project hosting services I
don't feel we'll be taking something away and not giving an alternative.

*  No, I don't volunteer. Not for this format of the wiki. But I do
volunteer for an alternative matching the outline I've suggested. 

* Mocking me is not right response, you know. The problem exists, you
fail to acknowledge it, but I don't care that much.

* Alex calls it hyperbole, I call it the simple truth (and many others
would second me). 

## The Plan

Many people commented that my post is not worth a damn if I'm not
willing to back it with action. I'm sad to disappoint my critics - but
I'll willing to go the whole nine yards on this one. Here's the
outline of my proposal for a new wiki:

1. Use [MoinMoin](http://moinmo.in/) as the wiki engine. It's written in Python and
it's GPL software. It doesn't use a database, it's featureful and
mature. It's successfully used by Debian and Ubuntu (and many other
respectable software organizations). I'm against using a Git backed
systems since it will increase the entry bar for user
participation. I'm even more against the use of a custom platform
developed specially to serve as the EmacsWiki.

2. I'll pay for the hosting and the new domain. I'd suggest that the
new project begins with the domain emacswiki.net or emacswiki.info and
eventually we'll assume the old emacswiki.org domain as well (should
the new wiki be successful enough). Suggestions for another name are
welcome in the comments section.

3. I and anyone willing to lend a hand will pick the articles worth
saving from the EmacsWiki and migrate them to the new one. I and
anyone willing to serve as moderator will monitor new contributions
afterwards.

4. Wiki entries will have a more or less standard structure and will
adhere and community established guidelines.

5. The old EmacsWiki will eventually be retired to another domain such
as old.emacswiki.org (or similar) for historic purposes and benefit of
users of old Emacs versions.

It this good enough for you to call it an action plan? Comments on it
are most welcome!

## Epilogue

I'm sorry that I'm the guy that has to break the terrible news to all of
the delusional EmacsWiki supporters out there - _It's not
special. It's not a beautiful or unique snowflake. It's the same
decaying wiki matter like some many else._ I'm sorry for my terrible
English and my lack of good manners. I'm sorry I'm willing do to
something while so many of you are just whining and ignoring the
existing problems.

I think as a member of the Emacs community I've shown my worth so far
and I'll willing to do even more. But I cannot carry out such a
massive undertaking on my own. I encourage everyone serious about
helping out to comment the article (here, not on reddit or hacker
news) or send me a personal email.

