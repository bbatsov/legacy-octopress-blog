---
layout: post
title: "Ruby or Python? Well, it depends..."
categories:
- Ruby
- Python
- Programming
---

**Disclaimer**

_If you're looking for a flame post - this is not one of them. I love
both languages and I'll simply compare some of their features and
possible uses._

## Prelude

Ruby or Python? This is the Question! Well it might not be the
Question, but it's a common question for many developers looking to
break free from the statically typed language they know and learn a
dynamic language. I personally know them both(though I know a bit more
Ruby, than Python) and in this article I'll share my personal opinion
on their strengths and weaknesses. You'd probably do good to learn
them both, but my arguments here may lead you to pick only one of the
languages depending on you preferences.

## Installation

**Linux/Unix installation**

If you're using a Linux distribution or some other Unix derivative
such as *BSD or Solaris you'll probably be able to install Ruby and
Python through the operating system's software management system. For
instance on Debian Linux systems(Ubuntu is a popular Debian
derivative) you can use apt to install them. Run the following
commands as root or with sudo:

``` bash
$ apt-get install ruby
$ apt-get install python
```

On Red Hat based distros like Fedora, CentOS, etc you can use yum
instead:

``` bash
$ yum install ruby
$ yum install python
```

You should keep in mind the fact that both Ruby and Python have two
version that are commonly used at the moment. Ruby's current version
is *1.9.2* and Python's is *3.2*. For various reasons(like backward
compatibility for instance), however, the current versions are not
widely deployed yet(especially Python 3). In most Linux distributions
the package ruby will actually be Ruby 1.8.x and the package python
will be Python 2.7.x. If your distribution is one of those - look for
packages named ruby19(or similar) and python3:

``` bash
$ apt-get install ruby19
$ apt-get install python3
```

or on a Red Hat system:

``` bash
$ yum install ruby19
$ yum install python3
```

Using the distribution package management system is a simple solution,
but in the case of Ruby it might not be best one. Most Ruby hackers
favour a powerful bash script called RVM(Ruby Version Manager) that
allows you to install several different version(or flavours of Ruby)
and switch easily between them. Please refer to the official
[RVM documentation](https://rvm.beginrescueend.com/) for installation
and usage instructions.

**Windows installation**

Installing Ruby on Windows used to be a pretty hard task, but this is
no longer the case now thanks to
[the RubyInstaller for Windows](http://rubyinstaller.org/). This is a
self-contained Windows-based installer that includes the Ruby
language, an execution environment, important documentation, and
more. It has two editions one for the older 1.8.x Ruby branch and one
for the current 1.9.x.

Python has several installation options for Windows - the most obvious
being the
[official Python installer for Windows](http://python.org/ftp/python/3.2/python-3.2.msi). [ActiveState's ActivePython](http://www.activestate.com/activepython)
is another popular option packed with more features, but you should
keep in mind that although the Community Edition is free ActivePython
is not an open-source project. Personally I prefer ActivePython. Other
prebuilt Python binaries for Windows are also available, but are not
commonly used.

**OS X installation**

Ruby is generally preinstalled on OSX, but OSX users can also install
it via [homebrew](http://mxcl.github.com/homebrew/) or RVM(as mentioned in the Linux section).

The is an official [Python package for OSX](http://python.org/ftp/python/3.2/python-3.2-macosx10.6.dmg) available. Most users
will probably prefer using homebrew, however.

## Syntax & code structure

Ruby makes heavy use of braces and keywords(like do/then/end) to
delimit blocks of code. Python relies simply on indentation.

``` python
def fact(n):
    return reduce(lambda x, y: x * y, range(1, n + 1))
```

Same thing in Ruby:

``` ruby
def fact(n)
  (1..n).reduce(:*)
end
```

I personally prefer the Python approach since it enforces the code
semantics based on the code structure alone without imposing special
syntax.

As a side node you might take under consideration that the Ruby method
definition doesn't have an explicit return value. The value of the
last expression in the method's body becomes automatically the
method's return value. Lisp developers will find this familiar. Java
and C# developers will probably find it a bit confusing. There is a
`return` in Ruby, though, it's just rarely used.

Both languages have support for nested function definitions.

Both languages have support for "top-level" functions - that live(or
seem to live) outside classes and modules(something not possible in
Java for instance). This makes them good for general purpose
scripting. While I would still prefer to do my system administration
with shell and Perl scripts - Ruby and Python offer a solid
alternative. Python has a richer system administration library so I'd
prefer it over Ruby for such tasks.

Ruby has a lot of crust("heritage") from Perl - like a myriad of
special variables that are now more or less deprecated. It also has
much syntactic sugar - for instance do/end is commonly replaced by {}
for blocks that are only one line long, there is special syntax for
hashtables, whose keys are symbols, etc.

Since special symbols(non alphanumeric) are allowed in Ruby
identifiers Ruby uses them to impose some naming conventions to make
the source code a bit more readable in certain scenarios - for
instance predicate methods(those that return true or false) have names
that end with ?(usually) like even?, odd?, prime?, etc. Methods that
mutate the object on which they were invoked generally have the !
suffix - sort!, map!, etc. I find this a nice decision. In Ruby you
generally have many ways to achieve the same result:

``` irb
ruby-1.9.2-p0 > 1.even?
 => false
ruby-1.9.2-p0 > arr = [1, 2, 3]
 => [1, 2, 3]
ruby-1.9.2-p0 > arr.map { |x| x * 2 }
 => [2, 4, 6]
ruby-1.9.2-p0 > arr
 => [1, 2, 3]
ruby-1.9.2-p0 > arr.map! { |x| x * 2 }
 => [2, 4, 6]
ruby-1.9.2-p0 > arr
 => [2, 4, 6]
ruby-1.9.2-p0 > (1..5).reduce(:*)
 => 120
ruby-1.9.2-p0 > (1..5).reduce { |x, y| x * y }
 => 120
ruby-1.9.2-p0 > (1..5).reduce do |x, y|
ruby-1.9.2-p0 >     x * y
ruby-1.9.2-p0 ?>  end
 => 120
```

No such things in Python, however. Python's philosophy is one of
simplicity - no excessive syntax sugar, one true way of doing things.

Both languages have powerful features for organising code in
libraries. I would not go into any details on the subject here, but
I'll share with you the fact that I like Python's more.

Both languages come with a REPL in which you can do some exploratory
programming. Ruby's REPL(irb)  allows you
to do TAB smart completion(amongst other things) by default. To get
TAB completion in the Python REPL you'd have to execute this bit of
code first:

``` pycon
>>> import readline, rlcompleter
>>> readline.parse_and_bind("tab: complete")
```

Alternative you can just stick this code snippet in the
**~/.pythonrc.py** file(create it if it doesn't exist). If you are using
Windows adjust accordingly(you will have to figure out where
pythonrc.py is located there).

Ruby does not have statements - only expressions. This
basically means that everything(objects, method calls) evaluate to
some value(though the value might not be helpful always).

In Python there are some statements such as assignment and _if_. One
thing I dislike about the Python REPL is that it doesn't print None
values. Compare this bit of Python code:

``` pycon
>>> print("this is a test")
this is a test
```

to this Ruby snippet:

``` irb
ruby-1.9.2-p0 > puts "this is a test"
this is a test
 => nil
```

In the Python version we see only the side-effect(the printing), but
not the return value.

Python also ships with a minimalistic IDE called IDLE. If you don't
have it by default after a python installation on Linux probably
you're vendor decided to package IDLE as a separate package. IDLE
offers basic features like syntax highlighting, code completion and
integration with a debugger. It's a good tool for exploratory
programming, but I advise you to pick another tool for serious development.

## Naming conventions

The naming conventions for both Ruby and Python are mostly the same
which is good if you're using them both on a daily basis - less room
for confusion.

* variable and method names consisting of more then one word are
  written in lowercase with underscores separating the individual
  words like_this.
* Class names start with capital letter and follow the camel case
  naming convention LikeThis. Some of Python's core classes, however,
  violate this convention.
* Constants are generally written in all caps with underscores
  separating the individual words LIKE_THIS.

As I mentioned earlier it's customary to add ? as a suffix to
predicate methods and ! to mutator methods in Ruby. This convention is
not always followed unfortunately, even in Ruby's standard library.

## OOP support

Both Ruby and Python are famous members of the family of object
oriented languages. Unlike languages such as Java and C#, however,
Ruby and Python are pure OOP languages. There is no distinction
between primitive types(such as numbers, characters and booleans) and
reference types(classes). Everything in them is an object and in that
sense it's an instance of some class:

``` pycon
>>> type(1)
<type 'int'>
>>> type("string")
<type 'str'>
>>> type(20.07)
<type 'float'>
>>> type([1, 2, 3])
<type 'list'>
>>> type((1, 2, 3))
<type 'tuple'>
```

And in Ruby:

``` irb
ruby-1.9.2-p0 > 10.class
 => Fixnum
ruby-1.9.2-p0 > "string".class
 => String
ruby-1.9.2-p0 > [].class
 => Array
```

As you can see core Ruby classes tend to have a bit more standard and
descriptive names than their Python counterparts. You can also notice
that in Python for some task we use built-in functions like type,
instead of method calls. The built-in function will eventually result
in a method invocation(like "string".__class__ in the case of
type("string")), but I find this irregularity in the syntax a bit
irritating.

Method invocation is more flexible in Ruby - you can omit braces in
some scenarios. This is handy when you're designing a DSL or you're
trying to implement the uniform access patterns(data should be
accessed through fields and methods in the same manner(read this as
with no braces in method invocations)). On the other hand Python's
uniform syntax makes it easier to spot method invocations.

Both languages don't have operators - just methods. Ruby's OO support
seems to be a bit more mature and polished(at least to me), but
Python's has some touches as well. I particularly like the explicit
self references that are required when you try to access class
members. I'm not too found of the use of special sigils in Ruby to
mark instance(@) and class members(@@). Though they make them visually
distinctive I think we could have lived without them - I'm generally
not a fan of non-uniform syntax rules(and you guessed it - my
favourite language is Lisp).

Ruby's metaprogramming model arguably gives it an edge in the OOP
department, but I won't be discussing the metaprogramming issues here
since they are quite lengthy.

## Functional programming support

Functional programming has been on the rise lately and it's useful to
examine what kind of support both languages provide for it. Both have
support for lambda functions and respectively - higher-order
functions(functions that accept functions as parameters). Ruby has
code blocks, Python has list comprehensions(generally favoured over
higher-order functions). Both languages lack in their standard libs
the immutable data structures that generally are the code of most
functional programming languages. Here's a few example related to
filtering a sequence based on some predicate:

``` pycon
>>> filter(lambda x: x % 2 == 0, range(1, 11))
[2, 4, 6, 8, 10]
>>> [x for x in range(1, 11) if x % 2 == 0]
[2, 4, 6, 8, 10]
```

Ruby:

``` irb
ruby-1.9.2-p0 > (1..10).select { |x| x.even? }
 => [2, 4, 6, 8, 10]
ruby-1.9.2-p0 > (1..10).select &:even?
 => [2, 4, 6, 8, 10]
```

Ruby's functional programming support seems to be better to me, but
this is of course subjective.

## GUI programming

Python has tkinker by default - a wrapper around the Tk library(which
sucks in my humble opinion). Ruby doesn't have even this much. Both
have binding for the popular GUI toolkits such wxwidgets, GTK,
QT. From my experimentation with them I can tell you that you'll be
much better off with Python in that department. It's not wonder that
many GTK+ applications these days are implemented in Python. Most Ruby
bindings projects seem to be in a state of disarray, abandonment - I
guess we have to thank Rails for that. Most people think of Rails as
the only use of Ruby which is sad...

Ruby devs shouldn't despair however. JRuby(Ruby's port to the JVM) has
an excellent support for the superb Swing GUI framework and MacRuby
has great support for building Cocoa Apps for OS X. I personally think
that JRuby is the best Ruby distribution out there, but that's the
point of another post entirely.

## 3rd party library availability and installation

It's not secret that part of Python's philosophy is that it comes with
batteries included - meaning that it's standard library is vast and
covers a lot of common tasks. In case you can't find what you're
looking for in it you're left with an number of third party libraries
for Python whose number can only be described by the word epic and
that cover every task conceivable. [PyPi](http://pypi.python.org/pypi)
maintains an up-to-date list of Python packages.

You have several options in the department of python package
management. If you're using ActivePython you can use the excellent
[PyPM](http://code.activestate.com/pypm/) tool, which provides quick
installation of thousands of packages for many Python versions and
platforms for ActivePython distributions.

[EasyInstall](http://peak.telecommunity.com/DevCenter/EasyInstall) is another popular solution that works with the standard
Python distribution. Like PyPM it allows you easily search for and
install Python packages from the PyPI that are bundled in Python's
standard egg format(Jave developers might think of eggs as
jars). EasyInstall has splendid documentation so I won't go into any
details here.

[pip](http://www.pip-installer.org/en/latest/index.html) is a
replacement for easy_install. It uses mostly the same techniques for
finding packages, so packages that were made easy_installable should
be pip-installable as well.

pip is meant to improve on EasyInstall. Some of the improvements:

* All packages are downloaded before installation. Partially-completed installation doesn’t occur as a result.
* Care is taken to present useful output on the console.
* The reasons for actions are kept track of. For instance, if a package is being installed, pip keeps track of why that package was required.
* Error messages should be useful.
* The code is relatively concise and cohesive, making it easier to use programmatically.
* Packages don’t have to be installed as egg archives, they can be installed flat (while keeping the egg metadata).
* Native support for other version control systems (Git, Mercurial and Bazaar)
* Uninstallation of packages.
* Simple to define fixed sets of requirements and reliably reproduce a set of packages.

pip doesn’t do everything that easy_install does. Specifically:

* It cannot install from eggs. It only installs from source. (In the future it would be good if it could install binaries from Windows .exe or .msi – binary install on other platforms is not a priority.)
* It doesn’t understand Setuptools extras (like package[test]). This should be added eventually.
* It is incompatible with some packages that extensively customize distutils or setuptools in their setup.py files.

Linux users will also find a great selection of Python libraries
prepackaged for use with the distribution's package manager.

Ruby has an application that is more or less equivalent to EasyInstall
called [RubyGems](http://rubygems.org/)(gems are the standard way to distribute Ruby
libraries). Linux users can of course install Ruby libraries with the
distribution's package manager as well.

RubyGems has the following features:

* Easy Installation and removal of RubyGems packages and their dependents.
* Management and control of local packages
* Package dependency management
* Query, search and list local and remote packages
* Multiple version support for installed packages
* Web-based interface to view the documentation for your installed gems
* Easy to use interface for building gem packages
* Simple server for distributing your own gem packages
* Easy to use building and publishing of gem packages

Using RubyGems, you can:

* download and install Ruby libraries easily
* not worry about libraries A and B depending on different versions of library C
* easily remove libraries you no longer use
* have power and control over your Ruby platform!

A reader pointed out that about 23000 packages are available for
installation through RubyGems and 15000 through PyPI. This, however,
cannot be considered as a certain sign that there are more libraries
available for Ruby than for Python.

Although tools like EasyInstall and RubyGems are easy to use and quite
handy, I as a long-time Linux users dislike them a bit, since they
circumvent the distributions native package handling. Unfortunately
package maintainers cannot find the time to package every Python and
Ruby library available so I guess EasyInstall and RubyGems won't be
going anywhere soon and of course we have to consider Windows users
for whom such applications are of great value given the lack of
unified package management on Windows.

One thing to keep in mind about installing eggs and gems is that some
of them are implemented in C(usually for performance reasons) and are
locally built prior to their installation - an operation bound to fail
if you don't have a C compiler installed.

## Misc

In terms of performance of the default interpreters CPython and MRI
Ruby Python is the clear winner. One should note, however, is that there
are many how quality implementation of Ruby and Python for different
platforms where the performance situation differs wildly. For instance
Jython is much slower that JRuby. With the addition of invoke_dynamic
in JDK7(basically bytecode level support for dynamic method dispatch)
the performance of JRuby and Jython could potentially be improved
greatly.

In terms of overall usage, market share, job offers and sheer size of
the community and available libraries Python is ahead of Ruby as
well. One of the main supporters of Python is after all none other
than the mighty Google. Ruby has also the unfortunate luck to be
living in the shadow of a single application written in Ruby - Ruby on
Rails, that is arguably more popular than the language itself.

Tooling for dynamic languages is currently not as advance as the one
for static languages. People often joke that Python(Ruby) > Java(C#),
but Python + any python IDE < Java + IntelliJ
IDEA(Eclipse/NetBeans). Python and Ruby IDEs seem to be mostly on par
currently. I do all of my Ruby and Python coding in Emacs, but I do
like RubyMine and PyCharm.

Since they are often used for the creation of webapps one should
consider the deployment issue. Most web hosting companies provide
cheap Python hosting, but very few companies provide Ruby hosting.

## The Python 3 problem

Python 3 was a great undertaking that improved on a lot of aspects of
the language(for example Unicode support) and the standard library. To
do this it dropped backward compatibility, an act that slowed it's
adoption immensely. Three years have passed since it's release and
still most hosting providers, Linux distros and Python projects hold
on to the older 2.7.x Python branch.

This is a bit of tragedy since Python 3 is truly a great improvement
over Python 2. I mention this because most recent books are written
with Python 3 in mind, but if you land a Python jobs somewhere chances
are you'll have to use Python 2.x.x for the foreseeable future.

## Epilogue

Ruby and Python are two beautifully engineered languages capable of
just about everything. If you don't know any of them you'll do well to
learn at least one. If you know only one it might not be a terrible
idea to learn the other.

I haven't touched on many language features(like Python generators and
Ruby mixins), but to be honest I'm just tired of typing. One good
place to start your journey to Python is
["Dive into Python 3"](http://diveintopython3.org/). For Ruby
beginners I'd recommend a copy of
["The Ruby Programming Language"](http://www.amazon.com/Ruby-Programming-Language-David-Flanagan/dp/0596516177).

_P.S. If you like exploring different programming languages and you're
currently shopping for ideas on the subject of which language to learn
next you might find my recent article
["Programming languages worth learning"](/blog/2011/04/27/programming-languages-worth-learning/)
interesting as well._
