---
layout: post
title: Automatically execute programs after zsh login
categories:
- Z Shell
- Linux
---

Sometimes you may want to start a couple of programs just after an
interactive login to your favourite shell, which in my case would be
zsh.

For example - I use Emacs as daemon process(emacs --daemon). I cannot use an init
script to start it since the daemon is usable on a per user basis. The
solution in this case is really simple - just create a **.zlogin** file in
your home folder and put in it all the commands you want executed
after you've logged into the shell. In my case I put:

``` bash
emacs --daemon
```

there and as soon as I'm logged in, the Emacs daemon is up waiting for
incoming connections.
