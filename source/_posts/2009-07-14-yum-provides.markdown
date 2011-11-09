---
layout: post
title: "Find out quickly which package provides a certain library with
YUM"
categories:
- Fedora
- Linux
---

One of the most dreaded things that you can see while trying to run
some application or trying to install an rpm package is a message
saying that some required library is missing.

Generally this is not a big problem, because most often the library
that you miss is packaged in a package named similarly to the
library. Sometime however this is not the case... Suppose for example
that you're trying to install IBM JDK 5.0 on a Fedora 11 box. You'll
most likely get the following error message:

``` bash
error: Failed dependencies:
libstdc++.so.5 is needed by ibm-java2-i386-sdk-5.0-9.0.i386
```

and there is no package named libstdc++ that you can install, so how
can you find out which package do you need?

The answer is simple:

``` bash
$ yum provides libstdc++.so.5

Loaded plugins: fastestmirror, presto, refresh-packagekit
compat-libstdc++-33-3.2.3-66.i586 : Compatibility standard C++ libraries
Repo        : fedora
Matched from:
Other       : libstdc++.so.5
```

Pretty neat, eh?
