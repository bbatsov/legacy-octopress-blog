---
layout: post
title: "Using Emacs for Rails development: The perfect setup"
categories:
- Ruby
- Emacs
- Rails
---

**Updated 29/04/2011**

Lately, I’ve started digging more and more into Rails, preparing for
the start of a Rails powered project. Although there are some IDEs
offering decent Rails support(namely RubyMine, NetBeans, Komodo and
Aptana Studio) I have always preferred the comfort of Emacs for
various reasons. So naturally I embarked on a quest to setup a
suitable environment for Rails development in Emacs. After a couple of
days of searching and evaluating possible solutions I finally set up a
worthy environment. It consists of a couple of components –
[ruby-mode](http://svn.ruby-lang.org/cgi-bin/viewvc.cgi/trunk/misc/ruby-mode.el?view=log),
[inf-ruby](http://svn.ruby-lang.org/cgi-bin/viewvc.cgi/trunk/misc/inf-ruby.el?view=log),
[autopair-mode](http://code.google.com/p/autopair/),
[nxhtml-mode](http://ourcomments.org/Emacs/nXhtml/doc/nxhtml.html),
[yasnippet](http://code.google.com/p/yasnippet/) and
[rinari](http://rinari.rubyforge.org/).

As you probably have guessed by now _ruby-mode_ provides support for
editing ruby source files. The mode is pretty feature complete and
under active development, headed by none other than Matz(Ruby's
creator) himself. I can only assume that Matz is an Emacs user
himself. You can get it from the ruby svn repository if you're using a
version of Emacs older than Emacs 23(it's built-in there).

_inf-ruby_ is a mode that spawns and inferior ruby process(irb shell)
to which you can directly send code from the ruby buffer you're
currently editing. For instance - you can define a function and while
your cursor is inside it you can press C-M-x - the function definition
will be evaluated in irb automatically and you can test it there. This
is extremely handy!

_autopair-mode_ provides auto insertion of closing braces, quotes,
ends, etc. . Instructions how to setup both modes can be found
here. It's a much more generic version of the _ruby-electric_ mode
that used to do similar tasks, but just in Ruby buffers.

Although many people recommend adding pabbrev(a mode which
provides auto-completion) to the setup, I don’t recommend it – I find
the mode mostly annoying and stick to the old school dumb
auto-completion with M-/ . If you're shopping for autocompletion,
however, a much better and smarter choice would be a
RSense[http://cx4a.org/software/rsense/].

_yasnippet_ is a package that offers dynamically expandable code
snippets(template), quite similar to ones in TextMate. It's very easy
to add your very own snippets if you wish to.

_nxhtml-mode_ is a pretty comprehensive package for web development in
general. We need it for its excellent support for erb
templates(.rhtml, .erb.html) and of course xhtml and css. Lately it's
not been as actively developed as it used to be, but it's still a
pretty good mode. Alternatively you can use
[Haml](https://github.com/nex3/haml) and
[SASS](https://github.com/antonj/scss-mode) and forget about
nxhtml. Both have pretty decent Emacs modes available.

_rinari_ is a mode for Rails development – it contains rich
functionality such as the ability to easily navigate between models,
views and controllers in a Rails apfplication amongst other
features. Instructions how to set up rinari together with nxhtml-mode
can be found on rinari’s home page.

It’s always a good idea to add [ecb](http://ecb.sourceforge.net/)(the Emacs code browser) to the mix,
though this is entirely optional.

A lot of the stuff I discussed here are part of the
[Emacs Prelude](https://github.com/bbatsov/prelude) that I
develop and maintain. I urge you to use the Emacs Prelude as a starting point to
develop your very own customized version of Emacs. Prelude comes with a
few ruby-mode customizations, yari(ri integration for Emacs), haml and
sass modes, autopair, yaml-mode, yasnippet, css-mode, ecb and a lot of
other goodies(projectile being one of my favourites).

I hope you enjoy this setup and it helps boost your Rails productivity in Emacs.
