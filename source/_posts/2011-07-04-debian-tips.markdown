---
layout: post
title: "Debian post installation setup & tips"
categories:
- Linux
- Debian
---

# Overture

I've recently been using Debian a lot (mostly Debian Wheezy (aka
testing)), So I've decided to adapt my
[Fedora 15 post installation setup & tips](/Linux/Fedora/2011/05/31/fedora-15-tips.html)
article for Debian. Here are some of the common things I add to a
typical "graphical desktop" Debian installation as well as some tips
and tricks that you'll hopefully find useful. Btw, I highly recommend
you to use the [netinstall Debian distribution](http://cdimage.debian.org/cdimage/daily-builds/daily/arch-latest/amd64/iso-cd/debian-testing-amd64-netinst.iso) - that way you'll get an
up-to-date installation immediately and you won't have to download
huge installation images.

This article will be of use mostly to people using Debian as a desktop
OS (with GNOME as their desktop environment) - it doesn't discuss any server configurations.

# Tweak defaults

**Configure sudo**

sudo gives you a way to execute single commands as the superuser. You
can also do this with "su -c", but you have to quote the commands there,
which I don't like very much. To enable sudo for some account first
run the command:

{% highlight console %}
$ su -c "visudo"
{% endhighlight %}

The file /etc/sudoers will open up in a customized vi editor. Append
somewhere to the end of the file the following line:

`username ALL=(ALL) ALL`

You should replace *username* with your username.

# apt-get + apt-cache or aptitude

There are two common ways (and many others less popular or obsolete)
to manage packages on a Debian system these days - the simpler apt-get
+ apt-cache combo or the more advanced aptitude tool. I tend to prefer
using aptitude since it's a all-in-one solution - you could use it to both
query and install packages and has both a CLI and a curses interface.

It doesn't really matter whether you decided to use apt-get/apt-cache
or aptitude, but you shouldn't mix their usage - pick one and stay
with it.

# Install additional software

I generally install Debian from the netinstall images and don't
customize very much the default package set since it's so easy to
install everything you need afterwards.

**Install REAL text editors**

gedit is ok for causal text editing, but professionals like software
engineers and system administrators will definitely need something more:

{% highlight console %}
$ sudo aptitude install emacs vim
{% endhighlight %}

Personally I use Emacs most of the time and use vim only to edit
config files that require root access. If you need an advanced Emacs
setup my suggestion is the [Emacs Dev Kit](https://github.com/bbatsov/emacs-dev-kit).

**Install Z Shell**

It's no secret that I love the Z Shell - after all I
[rave about it](/Z%20Shell/2011/04/29/one-shell-to-rule-them-all.html)
quite often. It should come as no surprise that I happen to use it and
probably you should start using it as well:

{% highlight console %}
$ sudo aptitude install zsh
$ sudo vim /etc/passwd
{% endhighlight %}

Find the line about your account and change there **/bin/bash** to
**/usr/bin/zsh**. Alternatively you can use the chsh program to
achieve the same result:

{% highlight console %} 
$ sudo chsh
{% endhighlight %}

Afterwards start a new login shell and a simple wizard will
fire up asking you some questions to create a default .zshrc file for
you. Alternatively you can use the excellent [O My Zsh](https://github.com/robbyrussell/oh-my-zsh) config - I'm
very fond of it.

**Install guake(a drop down terminal)**

I spend a lot of time at the terminal and like to have one at my
fingertips always. Since I'm a GNOME user guake is the best option for
me:

{% highlight console %}
$ sudo aptitude install guake
{% endhighlight %}

**Install LibreOffice**

LibreOffice is currently the best Linux option for word processing,
spreadsheet handling and presentation creation. It's generally
installed by default if you select the "Graphical Desktop" option in
the installation wizard, but you can install the
most common components at any time with the following command:

{% highlight console %}
$ sudo aptitude install libreoffice-calc libreoffice-impress libreoffice-draw libreoffice-writer
{% endhighlight %}

LibreOffice uses hunspell to do spellchecking. An English dictionary
will be installed by default, but you'll need to install additional
dictionaries manually:

{% highlight console %}
$ sudo aptitude install hunspell-bg
{% endhighlight %}

This command will install the Bulgarian hunspell dictionary. You
likely don't need it so install some more helpful dictionary instead. :-)

**Install OpenJDK**

If you need to run Java programs/applets:

{% highlight console %}
$ sudo aptitude install openjdk-6-jre
{% endhighlight %}

If you're planning to do some Java development:

{% highlight console %}
$ sudo aptitude install openjdk-6-jdk openjdk-6-doc openjdk-6-demo openjdk-6-source
{% endhighlight %}

**Install Deluge torrent client**

The default Transmission torrent client is pretty basic. I recommend
you to replace it with the much more feature-rich deluge:

{% highlight console %}
$ sudo aptitude install deluge
{% endhighlight %}

**Install Inconsolata font**

I'm a software engineer and I obviously spend a lot of time reading
and writing source code. I'm very picking about the monospace font
that I use and currently Inconsolata happens to be my favorite:

{% highlight console %}
$ sudo aptitude install ttf-inconsolata
{% endhighlight %}

**Install GIMP**
A lot of you might need an image editor. GIMP is generally
considered the best option so you might want to install it:

{% highlight console %}
$ sudo aptitude install gimp
{% endhighlight %}

# Install additional patent encumbered/proprietary software

**Enable non-free repo**

Just add contrib and non-free to the list of your enabled repos. Your
first line in /etc/apt/sources.list should look like this:

{% highlight console %}
deb http://ftp.bg.debian.org/debian/ wheezy main contrib non-free
{% endhighlight %}

Then do a:

{% highlight console %}
$ sudo aptitude update
{% endhighlight %}


**Install proprietary codecs**

No MP3 support in Debian by default? And almost no video codecs?
Non-free to the rescue! Type this:

{% highlight console %}
$ sudo aptitude install gstreamer-plugins-ugly gstreamer-plugins-bad gstreamer-ffmpeg
{% endhighlight %}

**Install VLC**

With MPlayer's development in stagnation VLC has established itself as
the best video player for Linux recently. Installing it is as easy as typing the following command:

{% highlight console %}
$ sudo aptitude install vlc
{% endhighlight %}

**Install Adobe Flash Player**

Love it or hate it - you probably need it.

{% highlight console %}
$ sudo aptitude install flashplugin-nonfree
{% endhighlight %}

You can omit this if you're planning to use Google Chrome (on a 32bit system), since it
comes with Flash Player built-in.

**Install Skype**

In a perfect world everyone would be using Google Talk... In the real one:

{% highlight console %}
$ sudo aptitude install skype
{% endhighlight %}

**Install Oracle JDK**

OpenJDK is great, but due to licensing problems it's not quite the
same as the Oracle JDK. If you start experiencing strange problems
(mostly in Swing programs) you'd probably do well to try the Oracle
JDK instead. The magic incantation goes like this:

{% highlight console %}
$ sudo aptitude install sun-java6-jdk sun-java6-demo sun-java6-source sun-java6-plugin
{% endhighlight %}

Debian uses OpenJDK by default, so you'll have to do some more work to
tell it to start using Oracle JDK. The **alternatives** program allows
you to select between multiple installed versions of a program:

These commands will make alternative aware of the java binaries and
set high priorities to them which will make them the default Java
binaries. You can use "alternatives --config binaryname" to select
active binaries manually.

**Install Google Chrome**

Firefox is dying, Google Chrome is the new king of the
browsers. Download it from the [official site](http://www.google.com/chrome) and install it:

{% highlight console %}
$ sudo dpk -i ~/Downloads/google-chrome-stable_current_i386.deb 
{% endhighlight %}

Google Chrome will install a apt repository as well, so you'll receive
updates as soon as they arrive.

Alternatively you can use Chromium - Chrome's open source sibling:

{% highlight console %}
$ sudo aptitude install chromium-browser
{% endhighlight %}

**Install DropBox**

[DropBox](http://www.dropbox.com) is a great file sharing service
which allows you to sync files between all of your computers and
mobile devices(Android, iPhone, iPad, etc). It has a great Linux
client which I use all the time. It's available in the non-free repo
so you can install it like this:

{% highlight console %}
$ sudo aptitude install nautilus-dropbox
{% endhighlight %}

# Epilogue

Hopefully some of my setup has made your setup more enjoyable and more
productive. I'll update this article along the way if I stumble upon
other things that I consider to be generally helpful.
