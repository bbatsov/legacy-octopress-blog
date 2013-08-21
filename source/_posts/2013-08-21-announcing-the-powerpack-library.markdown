---
layout: post
title: "Announcing the Powerpack library"
date: 2013-08-21 16:17
comments: true
categories:
- Ruby
---

[Powerpack](https://github.com/bbatsov/powerpack) is a small Ruby
library containing (at this point) a few extensions to some core Ruby
classes. I guess that in a way one can say it's something like Rails's
ActiveSupport, but with much smaller scope.

Since extending core classes is nasty business great care has been
taken to do so *properly*. For one - Powerpack would not include its extension
methods if the target class already has method named the same way.

Additionally - you're able to selectively use the extension methods
that Powerpack provides.You can load the entire `powerpack` library:

```
require 'powerpack'
```

You can load only the `String` extensions:

```
require 'powerpack/string'
```

You can load only a specific extension like `String#format`:

```
require 'powerpack/string/format'
```

Powerpack was born from my work on the
[RuboCop](https://github.com/bbatsov/rubocop) static code
analyzer. From time to time I wished I had some of ActiveSupport's
methods (but was unwilling to use ActiveSupport for various reasons)
or some useful method I've come across in the standard libraries of
other popular languages(`String#format` was inspired from Java,
`Numeric#pos?` and `Numeric#neg?` were inspired from Clojure, etc). It
has been helpful to me and I guess it might be helpful to some of you
as well.

If you'd like to know more, have a look at the
[online docs](http://rubydoc.info/github/bbatsov/powerpack/frames).

I'd love to hear your thoughts about Powerpack in its current form and
suggestions about its future (more helpful extensions for
instance). Comments, tickets and [Twitter](http://twitter.com/bbatsov)
are at your disposal!
