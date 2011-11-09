---
layout: post
title: "Java.next() - The Groovy Programming Language"
categories:
- Java
- Groovy
---

## Java.next()

In a series of articles labeled "Java.next()" I'll be discussing
modern alternatives to the Java programming language for use with the
Java Platform. This is the first installment of the series - "The
Groovy Programming Language".

## Prelude

We all know and love the Java _platform_(note the emphasis on
platform) for a couple of obvious reasons. Most notably it features a
huge high quality standard library and a legendary execution
environment - the Java Virtual Machine(JVM). The JVM is known to
posses the following qualities:

* Runs on all major platforms
* Enterprise ready
* Extremely stable
* Extremely fast
* Highly customizable - many aspects of its work can easily be
  adjusted such as GC settings, heap settings, etc.

There is a terrific community around the Java platform that has
contributed an immense amount of high quality software vital to the
success of Java. Hibernate, Spring, Eclipse, NetBeans, the myriad of
Apache projects are all community efforts.

So far so good, but it's not all rainbows and unicorns in the land of
Java. The Java programming language is a common source of gripe
amongst many developers for various reasons. I'll list here some of
the more notable of them:

* It's not a pure OOP language(there is a difference between primitive
  and reference data types)
* It uses static typing(highly subjective topic, but commonly brought up)
* It doesn't have support for closures(which instantly kills half of
  functional's programming ideas such as higher order functions)
* It has limited meta programming capabilities(compared to Ruby and
  Lisp for instance)
* There is no concept of top-level procedures(outside of class
  definitions)(this makes Java unsuitable for creating "script" programs)
* Its syntax is too verbose
* It's not suitable for the creation of DSLs
* Its development is sluggish and restrained by the corporate promise of backward compatibility
* It's an imperative language
* Its parallel programming model is revolving mostly around locks and
  threads

Naturally there are some languages that alleviate some(most) of Java's
problems such as:

* Ruby
* Python
* Lisp
* Erlang
* Haskell

They all, however, lack(with their default implementations at least)
an execution environment that can match the JVM. They also lack Java's
immense amount of libraries currently available. When enthusiasts
started porting existing languages to the JVM this came as no surprise
- it was only logical. A good language get a good execution
environment. For instance some folks ported Ruby to Java which
resulted in JRuby, Python also got a Java port called Jython. Though a
lot of good has come from such ports they was also a price to pay. In
the case of Ruby and Python some libraries are not written in
Ruby/Python, but in C for performance reasons, which naturally leads
to problems when you factor in a Java implementation of the
language. There is also the fact that the JVM(currently) doesn't have
support for dynamic memory dispatching which is feature vital for
dynamically typed languages to get a decent performance. For this
reason Jython is notoriously slow. The JRuby team did a much better
work, circumvented a lot of the JVM limitations and actually managed
to create a Ruby implementation that in some scenarios beats the
performance of the standard MRI Ruby 1.9 with it's custom YARV virtual
machine implemented in C. JRuby will be the object of a further
discussion down the road. Some of the languages that were ported to
the JVM suffer from another problem as well - it's not straightforward
and efficient in them to reuse existing Java libraries directly.

I'd like to lead this discussion in another direction, however -
programming languages that were implemented from scratch with the JVM
as their execution environment. While there are many of those three
stand out and have gathered a significant momentum in recent
years. They will be the subject of this post and the following
two. Without further adieu I'd like you to meet Groovy, Scala and
Clojure.

We'll begin our discussion with Groovy...

**Disclaimer**

_Before I start I'd like to point out that my knowledge of Groovy is
limited compared to my knowledge of Scala and Clojure. Despite this I
decided to share my thoughts on the language because it's certainly one
of the most popular JVM languages out there. If I've made any errors
in the article I didn't mean to insult anyone with my ignorance and
I'll certainly be glad to fix them when someone points them out._

## A little bit of Groovy history

James Strachan first talked about the development of Groovy in his
[blog](http://radio-weblogs.com/0112098/2003/08/29.html) in August
2003. Several versions were released between 2004 and 2006. After the
JCP(yep, you read that correct - Groovy is actually a Java standard
which is great or scary depending on your point of view)
standardization process began, the version numbering was changed and a
version called "1.0" was released on January 2, 2007. After various
betas and release candidates numbered 1.1, on December 7, 2007, Groovy
1.1 Final was released and immediately rebranded as Groovy 1.5 as a
reflection of the many changes that were made.

In July 2009, Strachan wrote on his blog that "I can honestly say if
someone had shown me the Programming in Scala book by Martin Odersky,
Lex Spoon & Bill Venners back in 2003 I'd probably have never created
Groovy." Strachan left the project silently a year before the
Groovy 1.0 release in 2007. Leadership of the project was assumed by
Guillaume Laforge (Project Manager and JSR-241 Spec Lead). Under his
guidance Groovy thrived and his risen to be arguably the most widely
used JVM language apart from Java.

Currently the development of Groovy proceeds with a very fast pace and
the latest major update 1.8.0 was released just a couple of days ago.

## Installation & Getting started

**Platform independent installation**
These instructions describe how to install a binary distribution of Groovy.

* download a [binary distribution of Groovy](http://groovy.codehaus.org/Download) and unpack it into some file on your local file system
* set your GROOVY_HOME environment variable to the directory you unpacked the distribution
* add GROOVY_HOME/bin to your PATH environment variable
* set your JAVA_HOME environment variable to point to your JDK. On OS
  X this is /Library/Java/Home, on other unixes its often /usr/java
  etc. If you've already installed tools like Ant or Maven you've
  probably already done this step.

For instance here's the relevant information of my shell's
configuration:

``` bash
export JAVA_HOME=/usr/java/latest
export GROOVY_HOME=/opt/groovy-1.8.0
export PATH=$GROOVY_HOME/bin:$PATH
```

You should now have Groovy installed properly. You can test this by
typing the following in a command shell:

``` bash
$ groovysh
```

Which should create an interactive groovy shell where you can type
Groovy statements. Or to run the Swing interactive console type:

``` bash
$ groovyConsole
```

To run a specific Groovy script type:

``` bash
$ groovy SomeScript.groovy
```

#### Linux installation

Most Linux distributions provide Groovy through their integrated
package management system. On Debian(and derivatives like Ubuntu) you
can install it like this:

``` bash
$ sudo apt-get install groovy
```

On Red Hat systems the magic incantation looks like this:

``` bash
$ sudo yum install groovy
```

Personally I'd prefer the platform-independent installation method,
since some distribution package Groovy in a non-standard manner which
confuses IDEs for instance.

#### Windows installation

Groovy features a native [Windows installer](http://dist.codehaus.org/groovy/distributions/installers/windows/nsis/groovy-1.8.0-installer.exe).

## Meet Groovy

{% blockquote Praise for Groovy, http://groovy.codehause.org %}
"Groovy is like a super version of Java. It can leverage Java's
enterprise capabilities but also has cool productivity features like
closures, builders and dynamic typing. If you are a developer, tester
or script guru, you have to love Groovy."
{% endblockquote %}

Groovy is:

* is one of the two standard languages for the JVM(the other is Java
of course)
* is an agile and dynamic language for the Java Virtual Machine
* builds upon the strengths of Java but has additional power features inspired by languages like Python, Ruby and Smalltalk
* makes modern programming features available to Java developers with almost-zero learning curve
* supports Domain-Specific Languages and other compact syntax so your
  code becomes easy to read and maintain
* makes writing shell and build scripts easy with its powerful processing primitives, OO abilities and an Ant DSL
* increases developer productivity by reducing scaffolding code when developing web, GUI, database or console applications
* simplifies testing by supporting unit testing and mocking out-of-the-box
* seamlessly integrates with all existing Java classes and libraries
* compiles straight to Java bytecode so you can use it anywhere you
  can use Java

Some of Groovy's most compelling features are:

* Pure OOP language
* Mostly Java compatible syntax
* Optional typing
* No need to wait for a future version of Java to get:
    * Closures
    * Attributes
    * Smart switch
* Duck typing
* BigInteger based arithmetic
    * This deserves some special explanation because of a rather
      strange design decision in Groovy. Groovy will create a
      BigIntiger out of a large enough number literal, but it won't
      promote the result of an integer operation into BigInteger -
      the result will actually overflow, in contrast to the semantics of most
      other dynamically typed languages. Multiply 1000 * 1000000000
      and you will end up with -727379968 in Groovy.
* SQL, XML & Swing improvements
* Unified data access API

A core idea, guiding the design of Groovy, is making it easy to use for
existing Java developers. Groovy's designers have gone so far in that
direction that the Groovy compiler will happily compile most Java
source files without the need for any modifications. Groovy, however,
builds heavily upon the standard Java's syntax and you'll do well to
get a grip of Groovy's core idioms. Groovy's syntax in a nutshell:

``` java
// old school Java code, but also valid Groovy code
System.out.println("Hello, world!");

// idiomatic Groovy
println "Hello, world!"

// dynamic variable definition
def name = "Bozhidar"

// GString featuring string interpolation
println "Hello, $name"  // => "Hello, Bozhidar"

// statically typed variable
String songName = "Coding in the Name of"

println "Now playing - $songName"

String multiline = """this is a multiline
string. There is not need to embed
newline characters in it"""

println multiline

// method definition
def greet(name) {
    println "Hello, $name!"
}

// method invocation
greet "Bozhidar"
greet("Bozhidar")

// safe dereferencing
def showSize(list) {
    println "List size is: ${list?.size}"
}

showSize([1, 2, 3])
// this is the important part
showSize(null)

// a list
def beers = ["Zagorka", "Bolyarka", "Shumensko", "Ariana"]

// list access
println "My favourite beer is ${beers[1]}"

beers.each { beer -> println beer }

// imports can appear anywhere and support the creation of aliases
import static java.util.Calendar.getInstance as now
import java.sql.Date as SDate

println now()
// java.util package is automatically imported in Groovy so this is java.util.Date
println new Date()
println new SDate(2011, 5, 5)

// language support for regular expressions
if ("Hello, Groovy" =~ /\w+,\s\w+/) {
    println "It matches"
}

// range filtering with higher-order functions
(1..10).findAll { n -> n % 2 == 0}.each { n -> println n }

// map
def capitols = [Bulgaria: "Sofia", USA: "Washington", England:"London", France:"Paris"]

println capitols["Bulgaria"] // => Sofia
println capitols["France"]  // => Paris

// class definition
class Person {
    def name
    def age

    Person(name, age) {
        this.name = name
        this.age = age
    }

    @Override
    String toString() {
        return "Name {$name}, age {$age}"
    }
}

def me = new Person("Bozhidar", 26)
println me
```

From the brief overview you might have noticed that like Ruby and
Python Groovy has language support for commonly used data structures
such as lists, maps, ranges and regular expressions:

* List - def number = [1, 2, 3]
* Map - def countries = [BG: “Bulgaria”, DE: “Germany]
* Range - def range = 1..1000
* Regular expressions - def whitespace = /\s+/

You might have noticed another interesting feature in Groovy - the
ability to combine static type(like in Java) with dynamic typing(like
in Ruby and Python). The keyword _def_ is used to introduce
dynamically typed variables in Groovy.

Groovy comes with its very own standard library(GDK) which builds upon
the JDK(for instance the File and String classes are enhanced in
Groovy) and offer some new features like the Groovy's famous builders.

## OOP in Groovy

Groovy is a pure object oriented language. Everything is an object,
operations are methods, etc. Compared the Java the picture looks right
about this way:

* Similar capabilities to Java
    * Define classes, interfaces, enums, annotations

* Differences to Java
    * Classes (and interfaces etc.) public by default
    * Methods public by default
    * Property support within classes (auto-setters/getters)
    * Duck typing

Java developers should feel mostly at home.

## SQL and XML handling

Groovy offers some nice improvements over JDBC and JAXP for handling
database queries and XML parsing.

Groovy removes a lot of boilerplate when dealing with SQL queries
compared to the native JDBC API:

``` java
import groovy.sql.Sql
sql = Sql.newInstance("jdbc:mysql://host/db", "username", "password", "com.mysql.jdbc.Driver")
sql.eachRow("select * from tableName", { println it.id + " -- ${it.firstName} --"} )
```

This code is written for a connection to a MySQL database. You will
need to adjust all the parameters to newInstance to connect to your
database, especially username and password.  Finally the third line
calls the eachRow method of sql, passing in two arguments, the first
being the query string, the second being a closure to print out some
values.  Notice that in the closure the fields of "it" are accessed in
two different ways. The first is as a simple field reference,
accessing the id field of it. The second is the included Groovy
expression mentioned above.

So the output from a row might look like:

```
1 -- Bozhidar --
2 -- Maya --
3 -- Kate --
4 -- Valentine --
```

XML processing is common enough task in computing and Groovy's
developers tried to make it simple and straightforward as
possible. Let's parse the following file:

``` xml
<books>
    <book>
        <title>Dune</title>
        <author firstname="Frank" lastname="Herbert"/>
    </book>
    <book>
        <title>Dune Messiah</title>
        <author firstname="Frank" lastname="Herbert"/>
    </book>
    <book>
        <title>Children of Dune</title>
        <author firstname="Frank" lastname="Herbert"/>
    </book>
    <book>
        <title>A Game of Thrones</title>
        <author firstname="George" lastname="Martin"/>
    </book>
</books>
```

All the code we need to write is:

``` java
def books = new XmlSlurper().parse("books.xml")
books.book.each {
    println "Title = ${it.title}, Author: ${it.author.@firstname} ${it.author.@lastname}"
}
```

Ruby and Python developers probably aren't particularly impressed, but
I can only imagine the look on the faces of Java developers that are
generally required to write huge amount of boilerplate code when
dealing with XML.

## Builders

Groovy has special syntax support for List and Maps. This is great
because it gives a concise representation of the actual object being
defined, so its easier to keep track of what a program or script is
doing. But what about programs which contain arbitrary nested tree
structures. Surely, they are the hardest ones to keep track of what is
going on. Isn't that an area where syntactic help will be most
beneficial?

The answer is definitely yes and Groovy comes to the party with its
builder concept. You can use it for DOM-like APIs or Ant tasks or
Jelly tags or Swing widgets or whatever. Each may have their own
particular factory mechanism to create the tree of objects - however
they can share the same builder syntax to define them - in a concise
alternative to XML or lengthy programming code.

One use for builders is the generation of markup:

``` java
import groovy.xml.*

def page = new MarkupBuilder()
page.html {
    head { title 'Hello, Groovy!' }
    body {
        div {
            3.times {
                p "Groovy power!"
            }
        }
    }
}
```

Result:

``` xml
<html>
  <head>
    <title>Hello, Groovy!</title>
  </head>
  <body>
    <div>
      <p>Groovy power!</p>
      <p>Groovy power!</p>
      <p>Groovy power!</p>
    </div>
  </body>
</html>
```

Builders can also be used to create Swing GUIs. Here's a very small example:

``` java
import java.awt.FlowLayout

builder = new groovy.swing.SwingBuilder()
langs = ["Groovy", "Scala", "Clojure"]
gui = builder.frame(size: [290, 100], title: 'Groovy Swing') {
    panel(layout: new FlowLayout()) {
        panel(layout: new FlowLayout()) {
            for (lang in langs) {
                radioButton(text: lang)
            }
        }
        button(text: 'Perform Magic', actionPerformed: {
            builder.optionPane(message: "Feel the power of Groovy!").
                    createDialog(null, 'Message').show()
        })
        button(text: 'Quit',
                actionPerformed: {System.exit(0)})
    }
}
gui.show()
```

Run the code to see the resulting GUI!

## Groovy tooling

* IDE
    * [IntelliJ IDEA](http://www.jetbrains.com/idea/) - the ultimate
      Groovy IDE. It's excellent Groovy support is part of its open
      source Community Edition.
    * [Eclipse](http://groovy.codehaus.org/Eclipse+Plugin) - the most
      popular Java IDE has an actively maintained Groovy plugin
    * [NetBeans](http://netbeans.org/features/groovy/) - Like IDEA
      NetBeans features built-in Groovy support

* Groovy distribution
    * groovysh - A Groovy REPL for exploratory programming
    * groovyConsole - A GUI groovy shell with extended capabilities,
      that is handy for the development and testing of small Groovy scripts
    * groovyc - the Groovy compiler

* Build tools
    * [Apache Maven](http://maven.apache.org)
    * [Apache Buildr](http://buildr.apache.org)
    * [Gradle](http://gradle.org)

## Killer apps

* [Grails](http://grails.org)
    * Groovy port of Ruby on Rails
    * Leverages the best Java technologies
        * Hibernate
        * Spring
        * Tomcat
* [Gradle](http://gradle.org) - powerful build tool, considered by many vastly superior to
  Maven. Several high profile projects(such as Hibernate) already
  migrated their builds to Gradle.
* [Griffon](http://griffon.codehaus.org/) - a Grails like application
  framework for developing desktop applications

## Common use cases

Groovy is a general purpose language, but it's used for some tasks
more often than for others. It's extremely suitable for:

* web application development(usually with Grails)
* scripting(although you have to factor in the cold startup time of
  the JVM before you start writing all your scripts in Groovy)
* tests development - it's a common practice in many Java projects to
  have the tests written in Groovy
* GUI development(usually with Griffon)
* Rapid prototyping - you'd do a quick app prototype in Groovy as a
  proof on concept and then you'd create a Java application based on
  it
* Exploratory programming - the groovysh is a great way to test class
  capabilities, methods and ideas with almost zero overhead - no
  annoying compile/run cycles to slow you down

When performance is critical you'd probably want to avoid
Groovy. According to some benchmarks around the Internet(like
[this one](http://stronglytypedblog.blogspot.com/2010/02/java-vs-scala-vs-groovy-vs-groovy.html))
Groovy is much slower than Java for certain tasks. I, however, haven't
read any new benchmarks on the subject and have no idea how reliable
the old ones are and how relevant they are to the current Groovy
version.

## Future prospects

With so many languages being created all the time developers
naturally ask themselves the same question over and over again -
should I waste my time learning this language? Related questions seem
to be:

* Will it endure the test of time?
* Does it have a vibrant and committed community around it?
* Can I find professional support?
* Does it integrate well with out current infrastructure?
* Does it have good tooling?

After all most of the currently popular languages like Java, C# and
PHP are nothing spectacular on their own, but have a combination of
factors that worked in their favour to get them to the top - solid
companies behind them, many deployment options and just the right
amount of beefing up/simplifying C/C++ make existing developers transition to the
new languages a relatively easy and painless experience.

SpringSource(the company responsible for the creation of the popular
Spring framework, now a division of VMWare) employs most of the core
Groovy developers and offers both [Groovy and Grails support](http://www.springsource.com/developer/grails). The fact
that a company such as this one believes in the technology is very
important whey you're trying to sell using Groovy in your current
company. And if you're existing infrastructure is built around Java -
well, you have next to nothing to worry about, except maybe will Java 7
deliver the promised speed improvement for dynamic languages
implemented on top of it.

Presently the Groovy community is vast and rapidly growing. The
language itself - constantly evolving.

NetBeans and IntelliJ have built-in Groovy support, which is a big
testament to the language's popularity as well.

In a sentence I don't see Groovy disappearing or dying anytime soon
even if its original creator has lost faith in it.

## Groovy resources

* Books
    * ["Groovy in Action"](http://www.manning.com/koenig2/)
    * ["Programming Groovy"](http://pragprog.com/titles/vslg/programming-groovy)
* On-line resources
    * [Official documentation](http://groovy.codehaus.org/User+Guide)

## Epilogue

Groovy is a language aiming to bring dynamic productivity to Java
developer without introducing them to a steep learning curve. The
language is beautifully architectured and integrates seamlessly with
the existing Java libraries and infrastructure. My biggest gripe with
Groovy was the lack of advanced support for parallel and concurrent
programming. A few days before I wrote this article, however, Groovy
1.8.0 was released and it features the excellent library for parallel
programming [GPars](http://gpars.codehaus.org/). Groovy's performance
is not stellar at this point, but I guess
this will be improved upon in Java 7.

With its easy to grasp Java-like syntax Groovy is a solid contender
for the attention of Java developers. A growing number of Groovy
related job offerings is a sign of Groovy's acceptance as a industrial
strength tool.

Some people criticize Groovy for the lack of innovation and claim that
it's simply an amalgam of ideas borrowed from other languages. I don't
see nothing bad with that approach as long as the features are
tastefully combined. Groovy might not be the most elegant language out
there, but it's one of the most practical ones and will help you get
the job done.

---
_P.S. Coming up next is a discussion of the Scala programming
language._
