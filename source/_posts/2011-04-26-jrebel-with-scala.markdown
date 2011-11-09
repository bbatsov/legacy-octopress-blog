---
layout: post
title: "Incremental development with Scala and JRebel"
categories:
- Java
- Scala
- Programming
---

One of the things I love most about Lisp development is the ability to
develop applications in an incremental interactive manner - you write
one function, compile it, load into your current REPL session, make
some adjustments and repeat this process until you get satisfactory
results. You never stop to compile your project, you never have to
restart your application server. Without those distractions it's
easier to maintain your concentration and to remain in the *flow*.

With languages like Scala and Java, however, you cannot do this - at
least without a bit of external help. This help comes in the form of an
application called [JRebel](http://www.zeroturnaround.com/jrebel/), which basically reloads the classes in your
program as you make changes to them and recompile them. JRebel is a commercial
application and generally you have to pay to use it... unless you want
to you use it for Scala development, that is. ZeroTurnaround(the
company that makes JRebel) offers
[free licences to Scala developers](http://sales.zeroturnaround.com/wp-content/themes/zeroturnaround4.0/modals/applyForLicense.php)
and if you're one of them you should definitely get one.

Installing JRebel is trivial - generally you have to only extract a
zip file(or use an installer) somewhere and drop in the JRebel folder
the licence file that they have e-mail you. Afterwards you simply have
to integrate JRebel with your build system. JRebel can also be
integrated with IDEs, but I want cover this here. I use mostly
[Maven 3](http://maven.apache.org) and
[SBT](http://code.google.com/p/simple-build-tool/) so I'll show you
what to do for them. With Maven you have to add the following to the
*$MAVEN_OPTS* environmental variable:

``` bash
export MAVEN_OPTS=-noverify -javaagent:/home/bozhidar/work/jrebel/jrebel.jar
```

Since most people use JRebel for web development to avoid the need to
restart their application containers and Scala's most prominent
framework is [Lift](http://liftweb.net) you'd probably want to enable
the JRebel Lift plug-in as well:

``` bash
export MAVEN_OPTS=-noverify -javaagent:/home/bozhidar/work/jrebel/jrebel.jar
 -Drebel.lift_plugin=true
```

Stick this in your shell's init file and source it to make it
available in the shell.

Now when you start your web app with

``` bash
mvn jetty:run
```

And the continuous Scala compilation with

``` bash
mvn scala:cc
```

The compiler with pickup the changes you made and JRebel will reload
the changed classes behind the scenes. The development process this
way starts to feel a bit like using a scripting language such as Ruby
or PHP.

If you're using SBT you should modify the sbt startup script to
include the same options that I mentioned in the section about Maven
configuration. Mine sbt script looks like this:

``` bash
#!/bin/bash

java -noverify -javaagent:/home/bozhidar/work/jrebel/jrebel.jar
 -Drebel.lift_plugin=true -XX:+CMSClassUnloadingEnabled
 -XX:MaxPermSize=512m -Xmx512M -Xss2M -jar `dirname $0`/sbt-launch.jar
 "$@"
```

Another use for JRebel is the Scala REPL itself. When you start the
REPL from inside SBT for instance with the command:

``` bash
sbt console
```

changes to the imported classes will be reflected automatically
without the need to do a *:replay* or restart the REPL - something
reminiscent of the interactive Lisp programming I mentioned earlier.

So what are you waiting for? Go grab JRebel and speed up your Scala
development process.
