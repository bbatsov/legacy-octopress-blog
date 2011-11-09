---
layout: post
title: "Java.next() - Scala: The Revenge of the Static Typing"
categories:
- Java
- Scala
---

## Prelude

This is the second post from my series dedicated to modern programming
languages for the Java platform. Last time we've discussed the
[Groovy programming language](/Java/Groovy/2011/05/06/jvm-langs-groovy.html), which
is a member of the ever expanding family of dynamic programming
languages. The Scala programming language, that is the object of
today's discussion, is different beast entirely - not only it uses static
typing(like Java & C# amongst others), but it also puts a heavy emphasis on the type
system, functional and parallel programming.

In theory Scala runs both on the JVM and on the CLR(the .NET VM). The
Java port, however, receives a lot more attention by Scala's developers
and it probably accounts for close of to all of Scala's
deployments(especially in production).

This article is extremely hard to write for me. Unlike Groovy, I'm
deeply familiar with the language and would like to share quite a lot
with you. For obvious reasons I cannot go into much detail (otherwise
I'd have written an on-line book). You're encourage to follow up this
article by reading some of the excellent resources, mentioned near its end.

## A brief history of Scala

After having written hundreds of thousands lines of Java himself,
Martin Odersky, Professor at EPFL, was well aware of the frustrations
faced by Java programmers. He formed the vision of applying the best
knowledge of the academic research community to the problem of making
the Java programming experience better, even fun. His first pragmatic
step was Java Generics, seen as a major success by the Java
community (though we should mention that it was C# that first brought
generic programming to the masses). But for the full vision of scalable concurrent programming
to be achieved he saw that the basic Java syntax would need to
change. You simply couldn't get there from here. But a deceptively
simple shift in syntax gained better uniformity to the object-oriented
aspects of Java, and this in turn enabled a natural fusion with
functional programming concepts which are critical for tackling
concurrency. In 2001 Scala was born. The first official version was
released in late 2003. This year it celebrates its first
anniversary in a way (depending on what do you consider the birthday).

Scala stands for a SCAlable LAnguage. What does this mean? Scala is
designed to tackle solutions of wildly varying sizes - from small
scripts (programming in the small) to massive distributed enterprise
applications (generally programming in the large). Scala also means
_steps_ in Italian and this is the reason why most Scala books have
some form of steps on their covers (arguably this is the reason why
Scala is very popular in Italy and particularly in Milan).

The current production version of Scala is 2.8.1 with 2.9.0 being in
the release candidate stages.

## Installing Scala

#### Universal installer

Scala has an [universal installer](http://www.scala-lang.org/downloads/distrib/files/scala-2.8.1.final-installer.jar) that could be ran on every platform
with Java installed. You can run it from the console like this:

``` bash
$ java -jar scala-2.8.1.final-installer.jar
```

Alternatively, on most systems simply double clicking the installer
jar will run it(assuming you have a GUI environment and assuming that
the java command is associated with jar files - something that is
usually so by default).

#### Installing from binary archive

Just download the Scala distribution for [Unix, OS X and Cygwin](http://www.scala-lang.org/downloads/distrib/files/scala-2.8.1.final.tgz) or
the one for
[Windows](http://www.scala-lang.org/downloads/distrib/files/scala-2.8.1.final.zip)
and extract it somewhere. I'm a GNU/Linux user and I tend to extract
all third party apps in the /opt folder:

``` bash
$ sudo tar xf scala-2.8.1.final.tgz -C /opt
```

You'd also want to add the folder containing the Scala binaries
(compiler, REPL, etc) to your PATH environmental variable. Unix users
might add something like this to their shell startup script (like
.bashrc):

``` bash
export JAVA_HOME=/usr/java/latest
export SCALA_HOME=/opt/scala-2.8.1
export PATH=$SCALA_HOME/bin:$PATH
```

You should now have Scala installed properly. You can test this by
typing the following in a command shell:

``` bash
$ scala
```

Which should create an interactive Scala shell where you can type
Scala expressions.

To run a specific Scala script type:

``` bash
$ scala SomeScript.scala
```

#### Linux installation

Most Linux distributions provide Scala through their integrated
package management system. On Debian(and derivatives like Ubuntu) you
can install it like this:

``` bash
$ sudo apt-get install scala
```

On Red Hat systems the magic incantation looks like this:

``` bash
$ sudo yum install scala
```

Personally I'd prefer the platform-independent installation method,
since some distribution package Scala in a non-standard manner, which
confuses IDEs for instance.

## Scala at a glance

{% blockquote James Gosling, creator of Java %}
If I were to pick a language to use today other than Java, it would
be Scala...
{% endblockquote %}

{% blockquote Joshua Bloch, author of "Effective Java" and many of Java's core libraries %}
If Java programmers want to use features that aren't present in the
language, I think they're probably best off using another language
that targets the JVM, such a Scala and Groovy.
{% endblockquote %}

Scala basically is:

* SCAlable LAnguage
* Pure OO language
* Functional language
* Statically typed language
* A language that integrates seamlessly with existing Java code
* A great community

Scala's more prominent features are:

* Type inference
* Advanced type system
* Improved OO model
* Improved imports system
* Simplified visibility rules
* Suitable for scripting, GUI, enterprise
* Relies on immutable data structures by default
* Great support for building parallel applications
* Pimps (improves) a lot of standard Java classes using a technique
  called [implicit conversion](http://www.codecommit.com/blog/ruby/implicit-conversions-more-powerful-than-dynamic-typing).

## Static vs Dynamic typing

This is one of the oldest debates in computing and everyone with a
little bit of common sense knows that there is no definitive answer to this
so fundamental question. Both approaches have merits and drawbacks. In
recent years we saw a rapid explosion in the rate of growth of
dynamic languages which lead many people to believe that static typing
is something of the past and is headed down on the road to oblivion. I ,
however, very much doubt such a possibility. So, without further ado
here's my take on their pros and cons:

#### Dynamic typing

* Pros
    * Less verbose
    * Better metaprogramming capabilities - it's very easy in a
      language like to Ruby to modify a class at runtime for
      instance. Java developers, on the other side, can only dream for
      such things...
    * Duck typing allows to reduce immensely the coupling between your
      classes
    * Reduced development and deployment cycles - most dynamic
      languages are implemented as interpreters and this way you're
      spared the tedious compilation/redeployment cycles

* Cons
    * Some might argue that type declarations serve as an additional
      documentation and their lack (arguably) make the code harder to
      read. Of course, when you're following a decent naming
      convention (and by that I mean that you're using sensible
      identifiers) that hardly matters.
    * Slower performance - knowing all the types in advance,
      naturally, allows the compilers to generate faster code for
      static languages than for dynamic ones. Some Lisp compilers,
      however, offer performance that rivals that of statically typed
      programs, so it's reasonable to expect that the situation in
      this department will improve over time.
    * It's hard to create IDEs for dynamic languages that offer the
      same level of assistance as those for static languages. The
      problem stems from the simple fact that in a dynamic language
      the type of an object is known only at runtime and an IDE will have
      a pretty hard type guessing the types because of this fact. In
      my humble opinion the lack of all the fancy IDE features like
      reliable code completion and refactorings is one of the central
      reasons why statically type languages like Java, C# and C++ are
      still enjoying higher popularity than dynamic languages.
    * You need to write more unit tests, because many of the simple
      errors that the compiler of statically typed language will detect
      will manifest themselves only at runtime.

#### Static typing

* Pros
   * Mighty development environments, capable of compensating for a
     lot of the languages deficiencies. You always get correct
     completion suggestions (in a decent IDE that is), all type errors
     are caught as you type (except the runtime errors that is).
   * Reliable refactoring - you make some changes, you recompile the
     project, you instantly see whether everything is OK after the
     refactoring. One of the key reasons why enterprise projects are
     often implemented in Java and C#.
   * Maximum performance - when you know all the types in advance it's
     not particularly hard to generate the most efficient in terms of
     performance bytecode/binary
     code.
   * You don't need to write unit tests for errors that will be caught
     by compiler.
   * The type declarations arguably serve as an up-to-date
     documentation on which you can always rely.

* Cons
   * Poor metaprogramming support - statically typed system limit very
     much the magic you can do in you programs. Metaprogramming is
     actually considered a black art in many statically type
     languages. In a functional statically typed language higher-order
     functions can compensate a lot in that department. Scala happens
     to be one such language, Haskell - another.
   * Generally statically type languages are a bit more verbose -
     mostly because the code is full of type annotations (languages
     like Scala and Haskell, however, have found the cure for this
     ailment - [type inference](http://www.codecommit.com/blog/scala/what-is-hindley-milner-and-why-is-it-cool))
   * No support (in most statically typed languages) for duck typing
     causes you to often link classes in hierarchies that you'd rather
     avoid if you had the chance to. I should point out that languages
     supporting structural types are not suffering from these
     problems. Scala happens to support them from version 2.6.0.

## A whirlwind tour of Scala

#### Scala is expressive

``` scala
scala> val romanToArabic = Map("I" -> 1, "II" -> 2, "III" -> 3, "IV" -> 4, "V" -> 5)
romanToArabic: scala.collection.immutable.Map[java.lang.String,Int] = Map((II,2), (IV,4), (I,1), (V,5), (III,3))

scala> romanToArabic("I")
res2: Int = 1

scala> romanToArabic("II")
res3: Int = 2
```

#### Scala removes the incidental complexity

Scala removes the incidental complexity and cut right to the core of
the problem. Imagine that you want to find whether or not a string
contains uppercase characters. In Java you'd write something like
this:

``` java
public boolean hasUpperCase(String word) {
    if (word == null) {
        return false;
    }
    int len = word.length();
    for (int i = 0; i < len; i++) {
        if (Character.isUpperCase(word.charAt(i))) {
            return true;
        }
    }
    return false;
}
```

So much boilerplate code (loop, if) to express such a basic idea. In
Scala you'd simply write:

``` scala
def hasUppercase(word: String): Boolean = {
  if (word != null)
    word.exists(c => c.isUpperCase)
  else
    false
}

// or more compactly
def hasUppercase(word: String) = if (word != null) word.exists(_.isUpperCase) else false
```

Scala's code actually reads a lot like English language that makes
sense to humans - check if in _word_
there exists an uppercase character. Notice that is Scala _if_ is an
expression yielding a return value, unlike in many other languages.

#### Scala is concise

Consider this simple JavaBean (well, not exactly JavaBean to be
precise - it lacks a no param constructor) definition:

``` java
class Person {
    private String name;
    private int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

In Scala the equivalent definition looks like this:

``` scala
class Person(var name: String, var age: Int)
```

This is what I call a good signal-to-noise ratio.

#### Scala supercharges OO programming

Scala is pure OO language - everything is an object, operators are
actually methods, everything yields some result(even constructs such
as if), there are no static field and methods

#### Scala is power overwhelming

Want to implement a thread-safe mathematical service in Scala? No problem!

``` scala
import scala.actors.Actor._

case class Add(x: Int, y: Int)
case class Sub(x: Int, y: Int)

val mathService = actor {
  loop {
    receive {
      case Add(x, y) => reply(x + y)
      case Sub(x, y) => reply(x - y)
    }
  }
}

mathService !? Add(1, 3) // returns 4
mathService !? Sub(5, 2) // returns 3
```

Case classes are out of the scope of this post, but I guess you get
the basic idea.

#### Scala is duck friendly

Duck typing is nothing new for developers familiar with dynamic
languages. Its the concept that an objects type is defined not by the
objects class, but by the objects interface. This allows us to write
very flexible code that works on unrelated types (in the inheritance
hierarchy) that happen to share common methods. For instance in Ruby
we could write this code:

``` ruby
class Duck
  def walk
    puts "The duck walks"
  end

  def quack
    puts "The duck quacks"
  end
end

class Dog
  def walk
    puts "The dog walks"
  end

  def quack
    puts "The dog quacks"
  end
end

def test_animal(animal)
  animal.walk
  animal.quack
end

test_animal(Duck.new)
test_animal(Dog.new)
```

It will work just fine - trust me. Few statically typed languages can
boast something similar... and Scala happens to be one of them:

``` scala
class Duck {
  def quack = println("The duck quacks")
  def walk = println("The duck walks")
}

class Dog {
  def quack = println("The dog quacks (barks)")
  def walk = println("The dog walks")
}

def testDuckTyping(animal: { def quack; def walk }) = {
  animal.quack
  animal.walk
}

scala> testDuckTyping(new Duck)
The duck quacks
The duck walks

scala> testDuckTyping(new Dog)
The dog quacks (barks)
The dog walks
```

This is point in the article when Ruby and Python are starting to get
impressed. :-) (I should know - I've learnt about this feature after
I've written the first draft and got some negative feedback due to my
oversight).

#### Pimp my library

Want to make the compiler convert between types from time to time to
get access to some richer functionality? Nothing is easier in Scala:

``` scala
scala> implicit def intarray2sum(x: Array[Int]) = x.reduceLeft(_ + _)
intarray2sum: (x: Array[Int])Int

scala> val x = Array(1, 2, 3)
x: Array[Int] = Array(1, 2, 3)

scala> val y = Array(4, 5, 6)
y: Array[Int] = Array(4, 5, 6)

scala> val z = x + y
z: Int = 21
```

Scala arrays don't have a + method, but Scala Ints do. When the
compiler sees that the + method is invoked on an object that doesn't
have it, it starts searching for an implicit conversion to a type that
has it - like Int. Both arrays are converted to their sums and the
sums are added together in the end.

## Playing around

A good way to start exploring Scala is the REPL. Fire it up and type
along:

``` scala
scala> println("Hello, Scala")
Hello, Scala

scala> val name = "Bozhidar"
name: java.lang.String = Bozhidar

scala> Predef.println("My name is "+name)
My name is Bozhidar

scala> var someNumber: Int = 5
someNumber: Int = 5

scala> var names = Array("Superman", "Batman", "The Flash", "Bozhidar")
names: Array[java.lang.String] = Array(Superman, Batman, The Flash, Bozhidar)

scala> names.filter(name => name.startsWith("B"))
res6: Array[java.lang.String] = Array(Batman, Bozhidar)

scala> names.length
res7: Int = 4

scala> name.length()
res8: Int = 8

scala> import java.util.Date
import java.util.Date

scala> var currentDate = new Date
currentDate: java.util.Date = Wed May 11 15:03:20 EEST 2011

scala> println("Now is " + currentDate)
Now is Wed May 11 15:03:20 EEST 2011

scala> currentDate.toString
res10: java.lang.String = Wed May 11 15:03:20 EEST 2011

scala> currentDate.toString()
res11: java.lang.String = Wed May 11 15:03:20 EEST 2011

scala> currentDate toString
res12: java.lang.String = Wed May 11 15:03:20 EEST 2011
```

The REPL has an excellent TAB completion - I used it ofter. You'll
note from these examples the flexibility and the brevity of Scala's
syntax - no **;** to terminate statements (though you'll have to use ; to
separate more than one expression on a single line). The types of the
variables are inferred by the context, without the need to
specifically specify them - if you assign a string literal to some
variable the compiler will figure out on its own that the variable
must of type String (also note that Scala strings are Java strings -
at least on the JVM). You've got a lot of flexibility when you're
calling methods - you can omit the braces and the dot in some
scenarios - this makes it easy to create Domain Specific Languages in Scala.

The REPL outputs both the result of the expression you've evaluated
and the output from the evaluation (if any). The result from the
evaluation is assigned to automatically generated variables named resX
(res0, res1, res3) and you can refer to them later on.

## Object orientation purification

* Everything is an object - there are no primitive types in Scala,
  though the compiler will map some Scala types to primitive Java
  types for performance whenever possible
* No operators, just methods
    * `1 + 2 === 1.+(2)`
* No static fields & methods - replaced by companion objects (a
  singleton object named the same way as the class). What would be a
  static field of a static method in Java will be a companion object
  field/method in Scala. This makes the Scala OO model purer than that
  of some other languages (of course in languages like Ruby where
  classes are objects class variables and methods have more or less
  the same meaning and the model is just a pure if not purer).

* [Traits](http://www.scala-lang.org/node/126) - the evolution of interfaces
    * Traits are interfaces on steroids
    * They can contain state as well as behaviour
    * Think of them more as Ruby's mixins than Java's interfaces
    * They can be implemented on the fly by objects
    * They are too complex to be properly explained in one short blog post :-)

## Functional programming

Functional programming has many aspects, but to get the bulk of it you
need just two magical ingredients - support for functions as objects
and a nice array of immutable data structures. Scala, naturally, has
both. Traditionally OOP languages have rarely had much support for
functional programming, which makes it awkward to express some
problems in them. Steve Yegge wrote an excellent article on the
subject some time ago - ["Execution in the kingdom of the
nouns"](http://steve-yegge.blogspot.com/2006/03/execution-in-kingdom-of-nouns.html).

#### Return of the verbs

* Functions are first class objects
    * val inc = (x: Int) => x + 1
    * inc(1) // => 2

* Higher-order functions
    * List(1, 2, 3).map((x: Int) => x + 1) // => List(2, 3, 4)

* Sugared functions
    * List(1, 2, 3).map(x => x + 1)
    * List(1, 2, 3).map(_ + 1)

#### Closures

Closures are basically functions that have captured variables from an
external scope (variables that were not parameters of the
functions). Closures are often used as the parameters of higher-order
functions (functions that take functions as parameters):

``` scala
scala> var x = 10
x: Int = 10

scala> val addToX = (y: Int) => x + y
addToX: (Int) => Int = <function1>

scala> addToX(2)
res0: Int = 12

scala> addToX(6)
res1: Int = 16

scala> x = 5
x: Int = 5

scala> addToX(10)
res2: Int = 15
```

#### Functional data structures

Functional programming revolves around the concept of immutability -
nothing is ever changed - we have some input, we get some output and
the input is not changed in the process. Consider a simple operation
like an addition of an element to a list:

* the operation could modify the list to which the element is being
  added
* the operation can return a new list that is the same as the
  original, but has the additional element

Functional programming favours the second approach and Scala as a
functional programming language provides data structures with the
desired behaviour.

* List - think here of Lisp lists and not Java lists(unless you're
  thinking of Java linked lists that is)
* Maps
* Sets
* Trees
* Stacks

Scala doesn't force you into functional programming, though. Apart
from the List, which is always immutable, we have two types of all the
core data structures mentioned - immutable and mutable. The immutable
data structures are those imported by default to promote a more
functional programming style, but you can easily switch to the mutable
versions and program in an imperative manner.

``` scala
scala> import scala.collection.mutable.Map
import scala.collection.mutable.Map

scala> val phoneBook = Map("Bozhidar" -> 123, "Ivan" -> 456)
phoneBook: scala.collection.mutable.Map[java.lang.String,Int] = Map((Ivan,456), (Bozhidar,123))

scala> phoneBook += "Maya" -> 53434
res13: phoneBook.type = Map((Maya,53434), (Ivan,456), (Bozhidar,123))
```

#### List almighty

The list is a core data structure in functional programming because it is
recursively defined and therefore it's very suitable for use in
recursive algorithms. A list is composed of cons cells, each having
two components - the value it holds and a reference to a next cons
cell. The last cell points to a special value - Nil (which happens to
represent an empty list).

`1 | -> 2 | -> 3 | -> Nil`

Here's some things you can do with Scala's lists:

``` scala
scala> 1 :: 2 :: 3 :: 4 :: 5 :: Nil
res3: List[Int] = List(1, 2, 3, 4, 5)

scala> val names = List("Neo", "Trinity", "Morpheus", "Tank", "Dozer")
names: List[java.lang.String] = List(Neo, Trinity, Morpheus, Tank, Dozer)

scala> names.length
res4: Int = 5

scala> names.foreach(println)
Neo
Trinity
Morpheus
Tank
Dozer

scala> names.map(_.toUpperCase)
res6: List[java.lang.String] = List(NEO, TRINITY, MORPHEUS, TANK, DOZER)

scala> names.forall(_.length > 5)
res7: Boolean = false

scala> names.forall(_.length > 2)
res8: Boolean = true

scala> names.filter(_.startsWith("T"))
res9: List[java.lang.String] = List(Trinity, Tank)

scala> names.exists(_.length == 3)
res10: Boolean = true

scala> names.drop(2)
res11: List[java.lang.String] = List(Morpheus, Tank, Dozer)

scala> names.reverse
res12: List[java.lang.String] = List(Dozer, Tank, Morpheus, Trinity, Neo)

scala> names.sortBy(_.length)
res13: List[java.lang.String] = List(Neo, Tank, Dozer, Trinity, Morpheus)

scala> names.sort(_ > _)
res14: List[java.lang.String] = List(Trinity, Tank, Neo, Morpheus, Dozer)

scala> names.slice(2, 4)
res16: List[java.lang.String] = List(Morpheus, Tank)
```

#### Pattern matching

You can think of Scala's pattern matching as a super charged version
of switch, capable of matching on a variety of criteria and of
destructuring that matched objects. Here's a simple example:

``` scala
scala> def testMatching(something: Any) = something match {
     |   case 1 => "one"
     |   case "two" => 2
     |   case x: Int => "an integer number"
     |   case x: String => "some string"
     |   case <xmltag>{content}</xmltag> => content
     |   case head :: tail => head
     |   case _ => "something else entirely"
     | }
testMatching: (something: Any)Any

scala> testMatching(1)
res18: Any = one

scala> testMatching("two")
res19: Any = 2

scala> testMatching(2)
res20: Any = an integer number

scala> testMatching("matrix")
res21: Any = some string

scala> testMatching(<xmltag>this is in the tag</xmltag>)
res22: Any = this is in the tag

scala> testMatching(List(1, 2, 3))
res23: Any = 1

scala> testMatching(3.9)
res24: Any = something else entirely
```

Pattern matching gives you a new way to implement common programming
task. For instance consider the following trivial problem - computing
the length of a list:

``` scala
def length(list: List[Any]): Int = list match {
  case head :: tail => 1 + length(tail)
  case Nil => 0
}
```

Sure, it's not tail-recursive, but it's pretty neat. Now that I
mentioned tail-recursion I should probably say a bit more about
it. Recursive solutions generally look very nice in source form, but
performance-wise are not that great because each recursive call
creates a new stack frame and what's even worse is that stack frames
are limited - create too many of them and your program will blow
up. This doesn't mean that we should start coding everything
imperatively, of course. Some compilers have the ability to optimize
away recursive calls if the last thing that happens in the recursive
function is a call to the function itself. In the case of our function _length_,
unfortunately, the last call happens to be of the method **+** of the
object **1** (of class Int). We can improve the solution this way:

``` scala
def length(list: List[Any]): Int = {
  def lengthrec(list: List[Any], result: Int): Int = list match {
    case head :: tail => lengthrec(tail, result + 1)
    case Nil => result
  }

  lengthrec(list, 0)
}
```

Notice that we now have a nested helper method with a second parameter,
an accumulator value. This pattern often recurs when dealing with tail
recursion - we take the original recursive definition and introduce a
helper method using accumulator that is tail recursive. The outer
method just calls the helper method and waits for the result. The
Scala compiler will translate internally this recursive function into
a something like a loop and the performance will be greatly improved,
while preserving the clarity of the recursive approach.

Some languages (like Scheme) will always optimize tail calls. Because
of limitations in the JVM not all tail calls can be optimized in Scala
(for now), but
some tails recursion is better than none.

## Parallel programming

With the advent of multi-core processors concurrent programming is
becoming indispensable. Scala's primary concurrency construct is
actors. Actors are basically concurrent processes that communicate by
exchanging messages. Actors can also be seen as a form of active
objects where invoking a method corresponds to sending a
message. Actors are not a new idea - Scala's actor library draws heavy
inspiration from Erlang - a programming language notable for its
support for the development of distributed highly parallel systems.

The Scala Actors library provides both asynchronous and synchronous
message sends (the latter are implemented by exchanging several
asynchronous messages). Moreover, actors may communicate using futures
where requests are handled asynchronously, but return a representation
(the future) that allows to await the reply.

All actors execute in parallel by their nature. Each actor acts as if
it contains its own dedicated thread of execution.

Here's a very simple actor example. The echoActor runs forever and
waits for messages:

``` scala
import scala.actors.Actor._
val echoActor = actor {
    while (true) {
        receive {
            case msg => println("received: "+msg)
        }
    }
}

echoActor ! "Chuck Norris is the only real actor!"
echoActor ! "You don't find Chuck Norris - Chuck Norris finds you!"
```

Here the actor just waits for messages and responds to them by
printing them to the console. Since the article's size is already
quite impressive I won't go into any further details about the actors.

I want you to know that actors are not the only way to write parallel
programs in Scala. You still have access to the native Java (or .Net)
primitive like threads, locks, executors, etc. Another option is the
Scala implementation of Software Transactional Memory(STM) - a
parallel programming model made recently popular by the Clojure
programming language. Scala's implementation is a work in progress and
you can have a look a it
[here](http://nbronson.github.com/scala-stm/). STM is basically a
programming technique that lets you model concurrent operations in a
way similar to db transactions - you combine the critical code in a
transaction and if possible execute it and commit the transaction,
otherwise just rollback it and maybe try again after a while. Note that this is a
_great_ oversimplification of what's actually happening - for all the
gory details you should read the exhaustive documentation.

## Tools

We all know that even the best programming language can be rendered
useless by the lack of good development tools for it - powerful text
editors, integrated development environments, profilers, build tools,
etc. Scala is a relatively young programming language that became
really popular just recently and as a result there are still no
development environments for Scala as powerful as those for Java
(although since both languages use static typing eventually the
environments will be on par). Most popular Java IDEs features feature
some form of Scala support and most Java build tools as well.

* IDE
    * [IntelliJ IDEA](http://www.jetbrains.com/idea/) - the ultimate
      Scala IDE at the moment. It works quite well, but it's a bit
      buggy that the moment (which is to be expected of something with
      some many beta features).

    * [Eclipse](http://www.scala-ide.org/) - the most
      popular Java IDE has a Scala plug-in that
      until recently was mostly useless, but currently is being
      totally reworked and the next stable version will bring usable
      Scala support to the Eclipse users. The development of the new
      Scala plug-in is headed by none other than Martin Odersky
      himself. Don't bother using the older version at all - just grab
      the latest beta.

    * [NetBeans](http://wiki.netbeans.org/Scala69) - Presently the
      Scala support in NetBeans is a bit basic, but it's usable.

    * [Emacs ENSIME](https://github.com/aemoncannon/ensime) - Ok, I admit - Emacs is not actually an IDE
      per se, but it's still much more powerful than most IDEs. Emacs
      happens to have an excellent Scala mode, called ENSIME that
      gives you code completion, instant feedback, an integrated REPL,
      SBT integration, refactorings and other goodies in an Emacs
      package. The project attempts to be the equivalent of the legendary SLIME (
      an Emacs mode for Common Lisp) for Scala. ENSIME is integrated
      into the [Emacs Dev Kit](https://github.com/bbatsov/emacs-dev-kit)(maintained by yours truly).

* Scala distribution
    * scala - A Scala REPL for exploratory programming; it's also the
      Scala "interpreter" and the Scala class runner

    * scalac - the Scala compiler

    * fsc - fast Scala compiler. The Scala compiler is notoriously
      slow to start and fsc is a partial solution to this problem. The fsc runs
      as a daemon and waits to receive files to compile. Maven's
      scala:cc and sbt's ~compile continuous compilation task use fsc internally.

    * sbaz - The Scala Bazaar System, sbaz for short, is a packaging
      system developed to automate the task of mainaining a Scala
      installation. The program allows you to easily upgrade your
      installation as soon as a new version is available. You can also
      contribute your own packages, and make them easily available to
      other sbaz users.

* Build tools
    * [Apache Maven](http://maven.apache.org)
    * [Apache Buildr](http://buildr.apache.org)
    * [Gradle](http://gradle.org)
    * [SBT](http://code.google.com/p/simple-build-tool/)

## Killer apps

Scala presently doesn't have that many killer apps. Here are the most
prominent:

* [Lift web framework](http://liftweb.net/) - Lift is a web framework
  that has cherry-picked some of the best ideas from existing frameworks and
  added some novelties of its own to harness the capabilities of the
  Scala programming language.
    * Lazy page loading
    * Parallel rendering
    * Comet & Ajax
    * Wiring
    * Designer friendly templates
    * Wizard
    * Security

* [Play framework](http://www.playframework.org/) - Play focuses on
  developer productivity and targets RESTful architectures. It has
  both a Java and a Scala API. It's considered by many to be the first
  Java web framework that was actually made by web developers.

* [Akka](http://akka.io/) - A powerful library for writing concurrent applications
  using Actors, STM & Transactors. It has both Scala and Java API.

* [SBT](http://code.google.com/p/simple-build-tool/) - a powerful
  build tool

## Success stories

* [Twitter](http://www.artima.com/scalazine/articles/twitter_on_scala.html)  - you remember how often Twitter used to go down because of
  overloads and suddenly the problems stopped - no, this was the
  moment in which Twitter's backend was rewritten in Scala (that
  moment never actually came)... I have it on good authority that the
  problem was actually resolved by great improvements in their Ruby
  code base. But they use Scala there - Twitter had a Ruby-based
  queueing system that we used for communicating between the Rails
  front ends and the daemons that often crashed under heavy loads, and
  they ended up replacing that with one written in Scala.
* [Four square](http://www.scala-lang.org/node/5130) - Four square
  uses Lift as well
* [LinkedIn](http://www.scala-lang.org/node/6436)
* SAP
* [Guardian.co.uk](http://www.infoq.com/articles/guardian_scala)

## Comparison to Java

It's only natural that Java developers are interested in how Scala
stacks up to Java:

* Pros
    * Scala is fast, just as fast as Java. Some might wonder why this
      is a feature - they should take a look at the performance of the
      most of the other JVM langs and they'll understand. Granted, all
      of the performance benefits come from the use of static typing
      in Scala, but Scala's code is often as concise as the code
      written in a dynamic language like Ruby or Groovy.
    * Great Java interoperability
    * Scala removes a lot of the incidental complexity of programming
      and let's you express your thoughts directly in the source code
    * The syntax of Scala is mostly uniform and you can usually easily
      create new abstractions that look like language built-ins.
    * Scala features great support for parallel programming.
    * Runs on both Java and .Net (at least in theory)
* Cons
    * Some aspects of the language are fairly complex like the
      subtyping rules for instance. This will probably scare off some
      people, but I can assure you that this complexity is superficial
      and once you've grasped enough of Scala everything will fall
      into place and seem to you the most natural thing in the world.
    * Calling Scala from Java is not as easy as calling Java from
      Scala.
    * The core API is still subject to constant changes and most new
      Scala version are not backward compatible with the old ones
      (unlike in Java).
    * Scala's community (albeit very friendly and helpful) is current
      tiny compared to Java's. You might not get an assistance from
      the community as quickly as you'd get it for Java related
      problems.

## Resources

* Books
    * [Programming Scala](http://programming-scala.labs.oreilly.com/)
      - great free on-line book
    * [Programming in Scala](http://www.artima.com/pins1ed/) - the holy
      bible of Scala. The first edition is available for free on-line.
* Blogs & Websites
    * [Official web site](http://www.scala-lang.org)
    * [Daniel Spiewak's blog](http://www.codecommit.com/blog/)
    * [Daily Scala](http://daily-scala.blogspot.com/)
* Exercises
    * [99 Scala problems](http://aperiodic.net/phil/scala/s-99/)

## Epilogue

Scala's future is nothing but bright. It uses static typing, which is
familiar to so many Java and C# developers, and is also the
prerequisite for creating very helpful IDEs. Scala runs on the
venerable Java platform and easily leverages all of its power while
adding a lot of magic of its own - implicits, type inference, pattern
matching, functional programming support, actors and others.

It's my personal opinion that if any language has the chance to
displace Java as the king of the world - that might be Scala. In all
likelihood this will never happen - rarely has the greatest solutions
enjoyed the greatest popularity (remember the Betamax vs VHS?). I do
believe, however, that Scala will capture a significant market share
in the coming years - mainly due to it excellent support for building
distributed systems.

Until next time and the next chapter of the story, dedicated to the
rising star of the JVM world - Clojure.
