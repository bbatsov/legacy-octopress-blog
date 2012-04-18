---
layout: post
title: "MELPA - homebrew (Emacs Edition)"
date: 2012-04-06 18:04
comments: true
categories:
- Emacs
---

A few weeks ago I wrote an
[article about the state of package management in Emacs](http://batsov.com/articles/2012/02/19/package-management-in-emacs-the-good-the-bad-and-the-ugly/). In
that article I pointed out that on the side of [package.el](http://wikemacs.org/wiki/Package.el) too much
was riding on the poorly maintained Marmalade repo. Today
Marmalade went dark (again) and many people are wondering what to do
now. The answer is simple - start using [MELPA](http://melpa.milkbox.net/) instead.

I was thinking of starting a project similar to Marmalade to alleviate
its problems, but then the MELPA project was brought to my
attention. This project follows the Homebrew (unofficial OSX package
manager) model of using simple GitHub collaboration to maintain and
grow a bunch of build recipes. In the case of MELPA, those recipes
show how to bundle upstream source packages into package.el-compliant
packages. The recipes can be tested locally by package authors, and
they are run hourly on the MELPA server to create an HTTP package
archive that Emacs users can simply add to their `'package-archives`
list. As [Phil Hagelberg](http://technomancy.us) said - there's no reason to drag in
complicated dependencies like Node for something that's essentially a
pile of static files. MELPA on the other hand is written mostly in
Emacs Lisp and is thus much more comprehensible to casual Emacs hackers.

Most packages currently contained in MELPA are development snapshots,
but the project maintainer
[Donald Curtis](https://github.com/milkypostman) and
[Steve Purcell](http://www.sanityinc.com/) (aka `sanityinc`) are
working on extending the MELPA build scripts to support stable
packages, using upstream version tags.

Adding a new package to MELPA is as simple as adding a few lines of
code to the `pkglist` file in MELPA's source code repo:

```cl
(name :url "<repo url>" 
 :fetcher [git|svn|darcs|wiki] 
 [:files ("<file1>", ...)])
```

You simply have to fork the [official repo](https://github.com/milkypostman/melpa), modify `pkglist`, send a pull
request and `package.el` compatible packages will be built
automatically for you on MELPA's server (you can also build the
packages locally to test if everything is OK with your recipes). Sure it's not as easy as
submitting a package via a web UI, but it's a much more robust
approach. It also eliminates a common problem in Marmalade - there
only the original uploader (+ people selected by him) can update a
package. Often the original uploaders are very hard to find...

To use MELPA with Emacs 24 (or a recent version of `package.el`) just
add this to your `.emacs` (or equivalent):

```cl
(add-to-list 'package-archives
'("melpa" . "http://melpa.milkbox.net/packages/") t)
```

There's a lot more info regarding MELPA on its official website and
I'd rather not duplicate it here.

I would encourage package authors and users to investigate and
contribute to MELPA. I've already submitted a bunch of packages
there and rebased [Emacs Prelude](http://batsov.com/prelude) to
use MELPA instead of Marmalade.

Together we can turn MELPA into the most extensive and robust community-supported
`package.el` repo! Emacs users deserve one of those :-)
