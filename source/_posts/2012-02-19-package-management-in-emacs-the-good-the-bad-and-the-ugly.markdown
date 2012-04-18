---
layout: post
title: "Package Management in Emacs: The Good, the Bad and the Ugly"
date: 2012-02-19 12:18
comments: true
categories:
- Emacs
---

## Prelude

Let's face it - although a vanilla Emacs installation is quite
powerful almost nobody is using Emacs without a pile of add-ons. And
managing those add-ons is quite frankly a pain in the ass. Traditional
options included installing Emacs add-ons via the operating system's
package manager (if available), downloading `.el` files from various
locations (everybody hates packages distributed only on Emacs Wiki
with no canonical version control repo) and simply sticking them on
the `load-path`, etc. It's more than obvious that such solutions are
less than ideal.

For instance if you're installing Emacs add-ons via a package manager
and you have to change OSes (or machines) you're mostly fucked. On the
other hand piling files manually in `.emacs.d` is equal to hell in the
version and dependency tracking department. There has to be a better
way, right? Wouldn't it be nice if Emacs had its own package manager
similar to the likes of `homebrew`, `apt` or `yum`?

[Emacs 24](http://batsov.com/articles/2011/08/19/a-peek-at-emacs24/)
finally introduces such a tool - its name is `package.el` (very
original, right?) and it's promise is to make you're lives a bit
easier. Does it manage to deliver on that promise? We'll see that in a bit...

<!--more-->

## Package management with package.el

`package.el` is bundled with Emacs 24, but it's not bound to Emacs
24. Before it became part of Emacs it was an external package, known
as ELPA (I guess that stood for Emacs Lisp Package Manager or
something similar). So even if you're an Emacs 23 user you can copy
the latest version of `package.el` from
[here](http://repo.or.cz/w/emacs.git/blob_plain/1a0a666f941c99882093d7bd08ced15033bc3f0c:/lisp/emacs-lisp/package.el)
and enjoy it. At this point you'll have to do something like:

``` cl
(require 'package)
(package-initialize)
```

Put this snippet of code near the beginning of your Emacs config,
since you'll definitely want packages installed via `package.el` to be
initalized *before* you start tweaking them.

What `package.el` basically does is that it connects to a list of
package repositories, retrieves the list of the packages there,
presents it to you in a interactive fashion and lets you install the
packages you like (of course you can also remove the once you don't
like). `package.el` understands the dependencies between packages and
if one package requires others to run they will be installed
automatically (which is really neat).

The magic starts with the command `M-x package-list-packages`. At this
point you should see something in the lines of this.

{% img /images/articles/packages-list.png %}

You can navigate the list of packages, mark the ones you want to
install with the "i" key or the ones you want removed with the "d" key
and when you're done you can press the "x" key to execute the
scheduled actions.

Initially `package.el` didn't provide the option to update a package,
but that should be fixed in recent Emacs builds. According to this
[thread](http://lists.gnu.org/archive/html/emacs-devel/2011-09/msg00371.html)
you can even update all of the installed packages by using the "U" key
in the packages list view (I guess that a small "u" would update only
one package). Unfortunately my build is lacking those capabilities so
I cannot comment of their usability.

You'd probably notice that your list of available packages is not
particularly long. That's because the official Emacs 24 package
repository has a strict licensing (and source code) requirements to
include a package there. Luckily there are a number of
community-maintained `package.el` repos around with much more relaxed
requirements. Probably the most popular of them is
[Marmalade](http://marmalade-repo.org/), created by
[Nathan Weizenbaum](http://nex-3.com/) of Sass and Haml fame. You can
include it in your `package-archives` list like this:

``` cl
(add-to-list 'package-archives
             '("marmalade" . "http://marmalade-repo.org/packages/") t)
```

Marmalade provides a web based UI for package upload and search (both
quite buggy unfortunately) and the ability to share the maintenance of
a package between several people, who'll be able to upload new version
of the package. There's also a Emacs Lisp Marmalade tool, that allows
you to submit packages directly from Emacs.

Using the `package.el` UI is ok if you're a casual Emacs user, but
what if you have a custom Emacs configuration, stored under version
control, that you'd like to instantly deploy on any OS/machine (like
Emacs Prelude). Here in play comes `package.el`'s programmer
interface. In
[Emacs Prelude](https://github.com/bbatsov/prelude) I use the
following code to install a list of required packages automatically on Emacs
startup (if necessary):

``` cl
(defvar prelude-packages
  '(ack-and-a-half auctex clojure-mode coffee-mode deft expand-region
                   gist groovy-mode haml-mode haskell-mode inf-ruby
                   magit magithub markdown-mode paredit projectile python
                   sass-mode rainbow-mode scss-mode solarized-theme
                   volatile-highlights yaml-mode yari zenburn-theme)
  "A list of packages to ensure are installed at launch.")

(defun prelude-packages-installed-p ()
  (loop for p in prelude-packages
        when (not (package-installed-p p)) do (return nil)
        finally (return t)))

(unless (prelude-packages-installed-p)
  ;; check for new packages (package versions)
  (message "%s" "Emacs Prelude is now refreshing its package database...")
  (package-refresh-contents)
  (message "%s" " done.")
  ;; install the missing packages
  (dolist (p prelude-packages)
    (when (not (package-installed-p p))
      (package-install p))))

(provide 'prelude-packages)
;;; prelude-packages.el ends here
```

This code check if all of the packages in the list are installed and
if any of them are not installed if refreshes the local package
database (in the case a required package for recently added to the remote
repo) and installs them.

To be able to publish a package to Marmalade (or another repo) it
should comform a standardized structure. A single-file package might look like this:

``` cl
;;; sass-mode.el --- Sass major mode

;; Copyright 2007-2010 Nathan Weizenbaum

;; Author: Nathan Weizenbaum <nex342@gmail.com>
;; URL: http://github.com/nex3/sass-mode
;; Version: 3.0.20
;; Package-Requires: ((haml-mode "3.0.20"))

;; Code goes here

;;; sass-mode.el ends here
```

A multi-file package should have an additional file named
`<name>-pkg.el` that should look like this:

``` cl
(define-package "sass-mode" "3.0.20"
                "Sass major mode"
                '((haml-mode "3.0.20")))

```

## The Bad and the Ugly

While `package.el` is great on paper, for it to really take off some
problems need to be resolved.

#### Updating should be easy

One of the best features of OS package managers is that they make it
really easy to update all of the installed packages to their latest
versions. Currently `package.el` doesn't support that (at least to my
knowledge), with the exception of the "U" key in the list packages
view. This seems to me like a pretty basic feature and I (and everyone
I've talked with) would really like to see it in Emacs 24 final.

#### Too much is riding on Marmalade

Marmalade has become extremely important in the recent months and the
list of packages there is growing every day. This would have normally
filled me with great joy, if it weren't for a few problems.

It seems that the project isn't getting much attention from its maintainer
(which is understandable, given the fact that he's maintaining several
high profile projects + the fact he's a full time Google
employee). As a result Marmalade is quite buggy (especially in the UI
department) and is missing key features, like the ability to contact a
package maintainer. At some point it was even lacking the ability to
delete a package. Uploads don't work reliably there, package refresh
sometimes yields http errors that require manual `M-x
package-refresh-contents` and from time to time there is even downtime
of the service.

The fact that its backend is written in Node.js (great technology, but
not widely understood for now) and hosted on Google
Code, doesn't improve the situation a lot. A Ruby or Python based
solution hosted on GitHub would certainly gain much more traction in
the community (and I'm planning to start work on one soon).

#### Scarce documentation

`package.el` is light on the documentation and you'll have to explore
its source code if you want to implement its required interface
(which luckily is very simple). I hope this will change by the release
of Emacs 24.

#### Too few package authors care about package.el

Package authors rarely tag versions that could be uploaded to a
`package.el` compatible repo and from time to time don't follow the
basic structure required. I always contact package authors to let them
know of such shortcomings in their packages and so should you.

## Alternatives

[el-get](https://github.com/dimitri/el-get) is another popular Emacs
add-ons management solution that has recently become popular.

el-get allows you to install and manage elisp code for Emacs. It
supports lots of differents types of sources (git, svn, apt, elpa,
etc) and is able to install them, update them and remove them, but
more importantly it will init them for you.

That means it will require the features you need, load the necessary
files, set the Info paths so that `C-h i` shows the new documentation
you now depend on, and finally call your own `:post-init` function for
you to setup the extension. Or call it a package.

el-get is inherently troublesome piece of software on Windows machines
and was originally designed to make it simple to obtain the latest
versions of packages from git - a practice which I profoundly
dislike. Master package branches are often buggy (but there are also
authors that never tag versions and rely on the rolling release model)
and I'm generally supportive of the stable version releases. While
some view it as a nice addition to `package.el` I feel that el-get is
too low level tool (in its approach to the problem) and should be
avoided.

**Update**

A few hours after I posted this article it got a nice lengthy comment
by el-get's author. Since I believe, that the comment is quite
interesting I'm adding it here without any alterations.

{% blockquote Dimitri Fontaine, Author of el-get %}
As the author of el-get, good article!  The Emacs extension situation
is far from ideal and needs hard critics so that work is done to
improve it.

I now want to share with you some of the features that are currently
only available in the development branch of el-get (soon to be
released as 4.1): you can now easily checkout a stable branch from a
git repository (thanks to the :checkout property) and you can even
setup which checksum you want installed.So when using git, the
checksum is in fact a revision, when using emacswiki you have to
compute the checksum (doing M-x el-get-checksum) and register it in
your el-get-sources setup, then if the file change on emacswiki el-get
will refuse loading it (hopefully until you've done your review then
updated the checksum).So while I perfectly understand your reserve
toward depending on el-get, I believe that your concerns are being
solved now.I would like to believe that authors of emacs lisp scripts
would take the time to consider formatting their sources for
package.el. Today it's far from granted, so by choosing ELPA you miss
a lot of things. And for the situation to change you need to have the
authors willing to package their extensions, or you have to fork their
work. With el-get you have access to 536 packages from the get-go, and
all of emacswiki (that's currently more than 1700 packages) after
you've done M-x el-get-emacswiki-refresh. As of writing this comment,
my M-x el-get-package-list contains 2106 packages ready to install,
almost all with descriptions.el-get is about social packaging where
it's easy to prepare a recipe for a package, whatever distribution
means its author picked. Then you can share that recipe very easily,
for example with el-get on github where we'll be happy to add your
work and have it installed by default when users either install el-get
or do M-x el-get-self-update.As for windows support, it all depends on
the packages you want to install. Most of them just work out of the
box, being a single emacs lisp file (.el). Some of them require to
have extra tools installed, from git or svn or mercurial to make and
autoconf. That's only how the authors are shipping their extensions
though, el-get is only providing for an integrated way to get at it.
We have accepted several improvements so that the windows experience
matches the others OS, and we consider windows a first class citizen
here.
{% endblockquote %}

## Epilogue

`package.el` is the future of Emacs add-on management - of that I'm
quite certain. It's far from perfect, but even in its present flawed
form it has already simplified the life of many Emacs users
immensely. I urge all of you to stop distributing Emacs packages via
sources such as the Emacs Wiki and to put a heavy emphasis on
`package.el`. Make your packages compatible with it, upload them to a
community maintained repo (or the official if possible) and keep them
up-to-date. Your users will love you for that!

I'd like to see a replacement to Marmalade in the future as well. A
more robust and polished solution, maintained by a team of several
people. Hopefully that moment is not that far in the future.
