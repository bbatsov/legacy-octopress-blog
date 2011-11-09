---
layout: post
title: "The Linux desktop experience is killing Linux on the desktop,
Part II"
categories:
- Linux
- Windows
- Rant
---

_Read this with an open mind._

## Prelude

A few days back I wrote a somewhat controversial article called,
["The Linux desktop experience is killing Linux on the desktop"](/Linux/Windows/Rant/2011/06/11/linux-desktop-experience-killing-linux-on-the-desktop.html). While
many readers seem to have grasped the true purpose of the article, a
lot of people claimed that it was nothing but FUD (a favorite term
of many people in the Linux community, who would rather ignore
existing problems than face/acknowledge them).

If you've read my last post and generally agree with it - don't bother
reading this one. It's basically more of the same - in greater detail
and with less profanities.

In this article I'll have a look at the state of the Linux desktop,
it's usability, strengths and weaknesses.

## Let's get some facts straight

I'm writing this post from my Emacs 23.2 client (in Markdown, to
publish it via git to my jekyll powered blog) connected to my Emacs
daemon, running on my Fedora 15 GNOME 3.0 desktop at home. This
machine has its every part carefully selected for maximum Linux
compatibility (the machine is a bit old, but that wasn't always the case) -
a GeForce 9600GT known to work "great" with the open-source nouveau
driver, an Asus Xonar DX sound card, supported by the great Oxygen HD
audio driver, etc. I do know how to buy hardware (contrary to popular
belief). Actually I've been a hardware
enthusiast for most of my life and I know much more about the inner
workings of computer components than most people. That said - the hardware that
I bought for my home PC was not the hardware that I wanted to buy, but
the one I had to buy.

Even the ill-fated T520 Sandy Bridge laptop was supposed to work very
well with Linux - after all Intel and Nvidia video cards are the
safest bet in town.

One of the great things about using a free (as in speech) OS like
Linux is that you get to do things exactly the way you want to do
them. You're in control. Everything is transparent. Nothing magically
happens behind the scenes. It's sad that this
doesn't extend to the ability to pick any piece of fairly generic
hardware and properly enjoy it. Often you just have to hope
and pray - and sometimes you might get lucky.

A reader pointed me to
[this piece](http://blog.eracc.com/2011/06/14/the-century-of-the-linux-desktop/)
- a rebuttal of my article. Here's an excerpt:

_Here we go again. Some fellow has gotten all whiny about being such a
big Linux fan, "… hardcore Linux user …", but he just had to go back
to Microsoft to get things done. Why? Because he is tired of having to
tinker with Fedora Linux to make things work, or fail to work, with
cutting edge hardware … and 64-bit Flash on 64-bit Linux is sucky …
and Skype on Linux is sucky … and … and … and. It was all just so
painful and time consuming he could not take it any longer and went
back to the safe arms of Microsoft to escape the horror that is
Linux. Good grief.
Okay, first and foremost, a true "hardcore Linux user", in my mind a
fan of Linux, is unlikely to switch from Linux to anything else. Oh
yes, he or she will switch Linux distributions in a heartbeat, or
maybe three heartbeats, if a distribution fails to work as needed. But
switching to Microsoft and leaving the Linux desktop behind? Not
likely, my friends. I consider myself a true "hardcore Linux user" and
I see no voluntary switch from Linux in my future … ever._

This bit produced a sad smile on my face. Had to go back to Microsoft?
Absolutely not! Chose to use Windows 7 (for the time
being)... If I was to go back to something it should have been FreeBSD
since it was the OS I was using before Linux (and of course Windows
before that indeed). I actually switched quite reluctantly from
FreeBSD to Linux for a simple reason - Linux supported wider hardware
variety and there were more native apps for it.

All Unix-derived OSes are more or less the same from an user's
perspective - mostly the same environment, the same applications. The
only thing that really makes the difference is the hardware support
and Linux is clearly far ahead of its competition.

Hardcore user? You bet! But hardcore doesn't mean an 'unreasonable
idiot, blinded by zealously'. It's not always that someone's favorite
technologies are the best solution to a problem. The section "the shit
I've endured" had a dual purpose - list a "few" problems and show how
resilient I am.

Distro hopping is something that mostly newbies do, because they fail
to grasp a fundamental thing in the land of Linux - 95% of the stuff
that comprises a distribution is generic stuff found in most other
distros. You cannot seriously expect that the same drivers in a
different distro will yield wildly different results... Sure, bugs do
tend to occur, and sometimes they are truly distribution
specific. Sure, some distros happen to patch the stuff they ship
heavily, while others favor shipping vanilla versions of both software ant
the kernel.

## The process of driver development

My former post placed a heavy emphasis on existing driver
issues. While I abhor some Linux drivers I've never ever blamed the
authors of open source drivers. Here's why:

The year and a half I've spent writing Linux drivers for a proprietary
Austrian company was some of the hardest time in my professional
career. Writing drivers is fairly hard task for two reasons - you have
to have very intimate knowledge of the hardware at hand and you have
to write very safe code (and carefully test it), because otherwise you might bring the whole
kernel down. I was basically reading tech specs (most boring read in
the world) most of the day and
writing very little code in end. Debugging drivers is not a pleasant
task either.

Linux certainly has some of the best developers in the world. I have
little doubt in that. The problem is that these same developers spent
their days working other jobs and you cannot seriously expect them to
have the time or the energy (not to mention the specs required) to
produce drivers that are on par with commercial counterparts developed
for OSX and Windows by big team with vast resources at their disposal.

This is the actual problem as I see it - we're expecting individuals
to create good drivers for us out the kindness of their hearts in
their little spare time with little or no hardware specs on which to
rely for absolutely no money.

I've read the source code of many network layer drivers in the Linux
kernel and I've noticed a common trend - a lot of the drivers were
actually written by hardware engineers (instead of software engineers)
- they are filled with copy/paste segments from other drivers, lots of
  useless/dubious/dangerous code. This doesn't surprise me - few
  software engineers have solid grasp of hardware and/or the will to
  take part in driver development. This is a big problem with no easy solution.

The hardware vendors are the only party that deserves blame for the
sorry state of many drivers. I cannot believe how hard it is for a
company with the size of AMD to deliver a decent Linux driver
for so many years. Their driver is a monument of everything that is
wrong with hardware vendors as far as Linux is concerned - no support
for latest kernels/X, no support for current state-of-the-art Linux
video technologies, notorious instability and performance. Nvidia fare
a lot better but still - their driver lacks the support basic stuff
such as KMS...

So what can we do? Obviously not everyone can start writing better
drivers, but still everyone could try to help...

For most desktop hardware vendors Linux is a non-existing OS. Linux
truly has a small market share, but that is not the actual
problem. The actual problem is that Linux desktop user would rather
wait for someone from the community to come up with a solution instead
of the pressure the vendors into action. Fill their mailboxes with angry
letters, write blog posts about their inadequacy to properly support
the third largest desktop OS in the world. Companies love to make
money and hate bad press...

## The desktop software stack

The Linux desktop stack has some great qualities - for instance it
often comes with batteries included. You have most of your day to day
need covered as soon as you install your distro - a decent browser, a
good email client, an office suit, disk burning utility, torrent
downloader, IM client, text editors, photo organizers, image editors,
etc. When I installed Windows 7 I was a bit surprised how bare the
initial installation is and how many third party apps I needed to
install. And of course most of the Linux desktop apps coming from the
same environment (KDE, GNOME, XFCE, etc) have a very uniform look and
feel to them which I personally value a lot.

Unfortunately not everything is great...

The Linux desktop application stack suffers from a few serious
problems:

* a few individuals make crucial decisions without taking any input
  from the user community
* many projects have only one principle developer that happens to do
  things his way without regard for anyone else
* often highly unstable beta quality software is pushed as stable to
  the end users
* a lot of prominent apps that are multi-platform seem to undergo
  sub-par testing/QA process under Linux and experience common problems
  like crashes and memory leaks that don't manifest that often on
  other platforms

In more details...

**Is it really better for the users?**

Often a new feature arrives that is marketed as a huge improvement for
the end-users. Most of the time the end-users are never inquired about
their opinion of the feature. PulseAudio is a great example. I was
pretty happy using ALSA directly, but nobody asked me what I thought
about the change. Initially it was fairly easy to disable pulse audio,
but as it became more and more integrated into the desktops the
process became harder (luckily pulse audio improved in the
process). While I'm perfectly aware of the technical reasoning that
lead to pulse audio's creation I do find it rather useless. With only
one major architecture left (almost no one uses OSS on Linux these
days) the introduction of intermediate sound layer of dubious quality
never made that much sense to me. Sure, ALSA needed a simpler API, but
we didn't deserve to be punished with pulse audio...

**It's my way or the highway**

Most of you probably remember that Pidgin (formerly Gaim) used to be
the default IM client in GNOME based distros. At some point this
quickly changed and Empathy became the default client. Part of the
reason for the switch was the unwillingness of the lead developer in the
Pidgin project to collaborate with the GNOME developers. I still
remember the controversial fix that made the input area non-resizable
with no option to go back to the previous setting. I guess GNOME's
devs were really pissed about something since they replaced the all around great
Pidgin with a vastly inferior and immensely buggy (at least for the
first year and a half) product.

Too much power of the hands of a single person with no overseer is
dangerous. In the open-source world one can easily fork a project, but
this is a dangerous path as well that is often likely to wreak havoc
into the development of the project.

**Are we your users or your beta testers?**

A few examples from recent years:

KDE 4.0

GNOME 3.0

Empathy

PulseAudio

NetworkManager

Beagle

The list could go on and on... Microsoft and Apple have certainly had
their fair share of mistakes (Win ME, Win Vista, OS X Leopard), but
nothing on a scale as epic as KDE 4.0 or GNOME 3.0...

**Some users are more important then others it seems...**

All those programs run on all major OS, but they perform worst on Linux:

Firefox

OpenOffice

Flash Player

Obviously writing great multi-platform apps is possible as illustrated
by software such as VLC and Google Chrome. But what about all the
rest. I feel that Firefox's days as the dominant browser on the Linux
desktop are numbered - most of my friends that use Linux have already
switched to Chrome (or the open source Chromium). Firefox on Linux is
like a bad joke - slow, memory hungry and unstable. I keep hearing
that it runs a lot better on OSX and Windows, probably because it got
a lot more testing on those platforms. I understand their reasoning -
most of their clients use those two OSes so it makes sense to make them
important in the dev/testing phases. But they should remember
something - Firefox is (for now) the default
browser only in most Linux distros and it's never going to be the
default in Windows or OSX...

Same goes for OpenOffice to the letter.

And flash is well -
flash. It's not the greatest piece of software on any platform, but
it's absolutely horrible in Linux. When I open a flash intensive web
site my CPU load generally spikes up to the sky (thank God for AdBlock
& FlashBlock).

Skype was not even mentioned here (until now obviously) since the Linux version is so far behind
the one for OSX and Windows that I wouldn't even consider it a
port. It's just some pile of crap compiled to be able to list Linux as
a supported OS on their website... They promised improvements, they
promised an open-source Linux client - two years later we're still
using Skype 2.1 BETA. I wish more people had the sense to use a
service like Google Talk so I wouldn't have to put up with skype at all.

## The community (communist) model

I live in a country from the former Soviet block (Bulgaria) and I've seen first
hand what Communism leads to. I've also seen first-hand why Communism
doesn't actually work - few people actually live and abide by it and
the rest of society simply practices the fine art of "getting by" and
lives on their shoulders. The Communism can only really work if
everyone is pulling their own weight in it (which sounds a bit absurd indeed).

Something similar is happening on the Linux desktop ship - everybody
says he's on board, but very few people are actually rowing and
bringing the Linux desktop to it's designated port.

I've written only two desktop project for Linux from scratch (an
English-Bulgarian dictionary utility and a GUI front-end for pacman on
Arch Linux), but I've contributed bug reports and patches to lots of
projects. No matter what your opinion about me is - I've done
something for the Linux desktop and I'm doing something for the desktop now
as well - writing this article...

What have you done? Sure, very few users are software engineers, but
that doesn't mean they can't help. Bug reports are just as important
as patches. Ideas and suggestions for improvements are highly valued
as well. Don't sit in the shadows doing nothing - step into the light
and do something to help your favorite project get a little bit
better.

Step by step. Fix by fix. Improvement by improvement. This is how good
software gets created.

The bottom line is - the more of us that pitch in the fight for a
proper Linux desktop experience, the bigger the chances of the dream
becoming reality become.

## Future

Unless something radically changes in the near future I don't see how
Linux can rise up to be a mainstream desktop OS. With very few
companies having any stakes in the Linux desktop that isn't happening
any time soon. I find a somewhat troubling trend in recent years - a
lot of companies that worked for a better desktop experience are now
gone. Ximian (the company behind GNOME) was purchased by Novell and
later Novell crumbled, making the future of one of the most popular
desktop distributions OpenSUSE doubtful. Mandrake was once one of the
most powerful Linux companies and Mandrake Linux was widely
used. Currently Mandriva is constantly on the brink of
bankruptcy. There are many other examples - Xandros, VidaLinux,
etc... Even the "mighty" Canonical struggles to build a successful
business model around their widely successful Ubuntu OS.

Desktop Linux has to be made somehow profitable for companies to start
investing more heavily in it. This is the hard, but honest truth. As
long as the primarily development is carried out with little (or no
funding), mostly by volunteers the hour of the desktop Linux will
never come.

There is one more serious problem - diversity. There are two many
distributions bring too little value to the table. The time spent
repacking the same software for a hundred distros could be better
utilized developing new applications/drivers and improving existing
ones. We need to have at least a couple rock solid desktop
distros/environments, otherwise the whole diversity thing means
basically nothing.

Few good options are worth more than a million half-baked options!

## Epilogue

This article (and the one before it) was never about jumping the
ship, claiming that Windows or OSX are better than Linux or spreading
"FUD" (if I totally hate a term this is the one). It was always about
raising the awareness of existing issues in the land of desktop
Linux. After all just a few days before [I had written a post
installation guide for Fedora 15](/Linux/Fedora/2011/05/31/fedora-15-tips.html).

While I was writing the last paragraph I got another GNOME 3 shell corruption (time
for killall gnome-shell to take the stage) on my totally supported
hardware... A skype sound notification interrupted the song I was
listening to (thanks a lot, PulseAudio)... And yet I'm still here. I
did switch to Windows 7 on my laptop and I do intend to use Window 7
at least for a while there. It's not perfect either, trust me about
that. Poor terminal emulator (though great PowerShell), a few random
application crashes (but these happen in Linux as well in recent
years) just to name a few.

The Linux desktop is at the edge of a cliff now. It's up to us to
decide whether we would save it or push it over the edge.
