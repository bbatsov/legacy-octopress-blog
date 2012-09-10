---
layout: post
title: "From Linux to OSX - 1 Year Later"
date: 2012-09-09 22:11
comments: true
categories: 
- misc
- Linux
- OSX
---

## Prelude

A little more than an year ago I wrote my rant post
[The Linux Desktop Experience is Killing Linux on the Desktop](http://batsov.com/articles/2011/06/11/linux-desktop-experience-killing-linux-on-the-desktop/)
and for the first time in 8 years I wasn't a desktop Linux user
anymore. I spent about a month wrestling with Windows 7, but let's
face it - Windows is ill suited for professional Ruby programmers like
me (and it's ill suited for most programmers, except maybe Java & .Net I
guess).

Anyways, it was never my intention to stick with Windows - I was just
doing my Mac due diligence. Now with 1+ year of OSX usage I'd
like to share a few things about my experience thus far with you.

<!--more-->

## From Linux to OSX

The transition was initially painful - I felt very odd dragging app
icons to the `Applications` folder to install them. To be honest I was
quite puzzled what was I supposed to do the first time I had to
install an app this way (it didn't have those helpful hints with the arrows most apps
do). The Linux distro package management is definitely infinitely
better, or at least it seems so from where I'm standing. Luckily for me most of the
tools I use are available from the third-party [homebrew](http://mxcl.github.com/homebrew/) package
manager for OSX. It's like an extremely basic version of the mighty
Gentoo `portage`, but it generally gets the job done.

On a more positive note - I was impressed with the quality and
responsiveness of the OSX desktop and the fact that Emacs keybindings
are used by default in its editor toolkit (and strangely puzzled by
the lack of right control key - how is one supposed to hit `Control +
a` I dare ask?). One app in particular - `spotlight`, blew me off the
water, especially after having dealt on Linux with crappy clones like
`beagle` in the past. Spotlight can truly find just about anything,
was it's own SQL-like query language and is **blazingly** fast.

I quickly found a good terminal emulator (that would be
[iterm2](http://www.iterm2.com/#/section/home) - it's actually the
best terminal emulator in the world IMHO) and
most of the command-line apps I used from day to day were already lying around
(after all OSX **is** Unix) - to my great surprise even stuff like PostgreSQL
(only on OSX Server) and `zsh` came preinstalled. Most of the other
apps I really needed had native OSX ports; the others - worthy
alternatives.

Having hated OpenOffice.org for many years I was very pleasantly
surprised by quality of apps like `Keynote` & `Words`.

Being a keyboard chap preaching in the church of `Das Keyboard` I was
a bit underwhelmed by the whole multi-touch mumbo-jumbo at first, but
after a while I came to the conclusion that Apple have the only
trackpads and mice that are actually worth using (even though I still
like using the keyboard way more).

To sum it all up - I got up to speed fairly quickly, but it was a
bumpy ride.

Here's a bit more details...

## The things I love about OSX

### The Desktop

It's pretty, it's quick, it's stable. It makes KDE4 and GNOME3 look
like school projects in comparison. And did I mention that the fonts
on OSX are even prettier than the ones in Windows?

### The OSX flavored apps

[Sparrow](http://sparrowapp.com/) is the first desktop mail client I ever liked (shame on
you Google for killing it). 

iTerm2 is the ultimate terminal emulator. It alone warrants the
purchase of a Mac.

Keynote is the best presentation program I've come to use thus far.

[Parallels Desktop](http://www.parallels.com/) is light years ahead of VirtualBox and KVM (as far
as desktop virtualization is concerned).

I could go on a lot like this, but I'll stop now.

It's obvious that Mac users have developed a taste in extremely
refined software.

### Hardware compatibility 

If something is supposed to work with OSX - it works superbly
out-of-the-box. I've almost forgotten now the days of constant battle
with crappy hardware. Sleep & Wake just work. Battery life is
exceptional (due to very advanced power management capabilities). 

Certainly controlling all of the hardware an OS will run on helps a
lot, but we still have to acknowledge Apple's achievement.

### Stability

One year, three Macs - only two or three system crashes. For a
developer that likes to tinker a little bit more than he should -
that's impressive.

That having said I had some Linux desktops that used run for more than
half an year without reboots (and the reboots were often caused by
power outages or distro/kernel updates). Linux stability on a (fairly
new) laptop? Well, that's a whole different story...

## The things that are OK

### The default apps

The apps bundled with OSX are not bad at all, but they aren't
particularly great. Still - Safari is a very good browser, Mail is a
much better desktop client than Evolution/Thunderbird, Calendar is a
good organizer (but a bit buggy when it comes down to Google Calendar
integration), Messages is so-so. 

The bottom line is - you can go a long way with the bundled apps, but
they aren't exactly perfect. My advice - shop for alternatives (both
open-source and proprietary).

### Mac App Store

Decent way to distribute proprietary apps, but with all the
restrictions on the app sandboxing there aren't many interesting apps
out there. Hopefully it'll get better in time. The ability to upgrade
your OSX by purchasing the new version from the App Store is very cool
(for a proprietary OS of course).

### Emacs

The Cocoa port of Emacs is a bit immature and there are some visual
glitches here and there (try out `M-x linum-mode` for instance), but
they are forgivable. I'm also missing the deep integration Emacs had with Linux.
And who the fuck designed all the official Mac keyboards without a
right control key? I finally understood why so many Mac users where on
vim :-)

Btw, remapping the `Caps` to `Control` is not the answer. I do it now,
I did it on Linux as well. You simply not supposed to hit Control +
any other key with the same hand. It's disruptive to your
typing... But then again - you should probably do most of your typing
will a full sized keyboard :-)

### Software Development

OSX doesn't nurture software development as much as Linux does, but it
comes pretty close in second place. All the tools you know and love
are available, but their installation & setup is a little bit more
involved on OSX. There is a reason why the screenshots in most
programming books show OSX.

### System administration

Definitely a step back from Linux. Programs like `launchctl` (for instance) are not
exactly fun to work with, but they do get the job done. I'd never use
an OSX box for anything more than a desktop workstation. Setting up a
sensible `$PATH` is not as trivial as it was on Linux either
(`/etc/paths` and some plist I forgotten come to mind).

## The things I hate

### The special keys

Not exactly an OSX feature, but still...

One year and I still hate `Command` and `Option` - option is basically `Alt`
on a strange location and Command is totally useless IMHO. I'd
probably wouldn't have hated them as much if there were room left on
the Apple keyboards (expect of course the old wired Apple keyboard) for an addition control key. Luckily for me I use an
external
[Das Keyboard Ultimate](http://batsov.com/articles/2008/06/16/das-keyboard/)
most of the time...

Command and Option do have some value, I'd probably would have
appreciated it if they didn't come at the cost of my beloved right
control (which I guess only Emacs users are missing anyways).

### No standard all mighty package manager

On Linux I had `aptitude`, `yum`, `portage` and `pacman` - all amazing at what
they do. On OSX - `homebrew` is a decent option, but it's a far cry from
the might and magic of the Linux package managers. Still, `homebrew`
is better than it's alternative, so beware!

### Ugly XML config files

Here and there in OSX you have to write some appalling [XML config
files](http://en.wikipedia.org/wiki/Property_list). I thought I'd never see the likes of those again after I put
Java development behind me :-)

### XCode

You need to install a giant lame IDE just to get a bunch of command
line development tools? That's one of the most annoying things I've
encountered up-to-date in OSX.

Yep, I know about the tools being available
[separately](http://kennethreitz.com/xcode-gcc-and-homebrew.html) for
couple of months now, but requesting an Apple developer registration
just to get them seems a bit to much to me. 

## Epilogue

Am I happier now without Linux? Definitely! Is OSX a better OS than
Linux? Absolutely not! It does have a **much** better desktop
experience and since I spend most of the time on a computer
interacting with the desktop - that's a big win for me. Of course I
wouldn't mind seeing Linux achieve this level of desktop maturity and
stability.

Should you dump Linux and join me in **darkness**? How the hell should
I know? :-) I'm just sharing my two cents - if you're happy using
Linux you should **definitely** stick with it. Obviously I wasn't and
there weren't that many alternatives lying around.

Not having to deal with hardware problems and immature desktop apps is
like a breath of fresh air and it more than compensates for the few
shortcomings of OSX. Nothing compensates the lack of that right
control key on most keyboards, but after all that's not an OS problem
;-)

There is great vibrant hacker community gathered around OSX and it's
one of the main driving forces of the OS. There is unfortunately a lot
of corporate pressure from Apple as well, but as you already know by
now - there are never perfect things, there are always
compromises. I'd rather use a proprietary OS that stays out of my way,
than a free OS into which I bump at every turn.

Soon I'll blog a little bit more about the practical aspects and
implication of the migration. Cheers, mates!

**P.S. I've updated the original post a bit to reflect some of the
initial feedback I received.**
