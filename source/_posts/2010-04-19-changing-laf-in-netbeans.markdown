---
layout: post
title: "Changing the look & feel in NetBeans 6.8"
categories:
- Java
- NetBeans
---

Recently I’ve been trying to switch my work environment theme to
something with lower contrast(notably the excellent zenburn theme for
emacs, vim, gnome terminal, gnome, etc). Swing
applications however have difficulties with GTK themes when they are
using the GTK+ look & feel so I’ve decided to go to Nimbus – the new
default look & feel for Java apps since Java 6 Update 10.

The only problem with the plan was that there is no way to change the
look and feel inside NetBeans – it had to be done by changing its
configuration. This is done fairly easy. Just find the file
/etc/netbeans.conf in NetBeans’s installation folder and append this to
the netbeans_default_options section:

`--laf Nimbus`

Now you just have to (re)start NetBeans and you can enjoy Nimbus. More
information about look & feels in NetBeans can be found here.
