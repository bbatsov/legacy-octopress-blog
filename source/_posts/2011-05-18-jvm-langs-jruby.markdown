---
layout: post
title: "Java.next() - JRuby: The Rubyists Strike Back"
categories:
- Ruby
- Java
---

## Prelude

So far in the Java.next() series I've discussed only languages that
were engineered from the start to run on the JVM ([Groovy](/Java/Groovy/2011/05/06/jvm-langs-groovy.html), [Scala](/Java/Scala/2011/05/08/jvm-langs-scala.html) and
[Clojure](/Clojure/Java/2011/05/12/jvm-langs-clojure.html)). However, a lot of good programming languages existed even
before the inception of the idea to run languages other than Java on top of
the JVM. Some notable examples are Ruby and Python for instance. Today
I'll be writing about [JRuby](http://jruby.org/) - the pure Java port of the Ruby
programming language (and undoubtedly the most advanced and widely
adopted of the 9 (!) actively maintained Ruby ports).

This post will differ somewhat from the others so far, because I won't
be spending any time to dwell on the basic Ruby syntax and will only
highlight the advantages over plain old Ruby that JRuby provides -
like calling Java code from a Ruby application and scripting Ruby from a
Java application.

## Why JRuby?

Ruby has long been known as one of the most elegant programming
languages out there. With the rise of the Rails web framework several
years ago the language was propelled into the mainstream and showed a
lot of common developers alternative (better) ways to get their jobs done with
less hassle and more grace. While the language is generally well liked
(albeit is has some syntax quirks and oddities, mostly courtesy of its
Perl heritage) its default execution environment MRI (Matz's Ruby
Interpreter) is not the object of international affection. As an
application written in C it suffers some portability problems (a few
years ago it was quite hard to get MRI to run properly on Windows and
even now you might run into some missing dll error from time to
time). MRI's performance is not stellar either and it even used to be
quite terrible before the advent of Ruby 1.9 which incorporated YARV
(Yet Another Ruby VM), which significantly improved its performance
(but still left a what to be desired). There is also the problem with
the missing standard portable GUI development library and the somewhat
limited deployment options because of MRI's limited
portability.

Matz's has often said that he's no VM specialist, he's a
language architect/designer and the beauty of the language concerns
him more than the performance of the reference implementation. He's
also said that he loves diversity and is certain that interested
parties will offer high quality alternatives to the standard Ruby
runtime.

When it comes down to a high quality runtimes few people don't start
thinking immediately about the Java platform, known for its infinite
(not literally infinite of course, but vast enough) libraries,
rock-solid and secure JVM and great support for compile-time and
runtime performance
optimizations. It's not unheard for a Java application to match and
excel the performance of a native C application by employing
techniques like _just in time_(JIT) compilation, hot spot detection and
optimizations, etc.

So it's only natural that at some point a bunch of people decided to
create a version of Ruby that could run on top of the acclaimed
JVM. This version of Ruby is (believe it or not) known as JRuby. With
JRuby you get the best of both Java and the Ruby worlds. Here are just a few possibilities:

* Deploy a Ruby on Rails web application to Google’s App Engine
service.
* Write a Rails web frontend to your existing Java enterprise
  application.
* Target the latest Android smartphones with your Ruby code using [Ruboto](http://ruboto.org/)
* Create cross-platform GUIs with Java's Swing (or SWT)
* Build your project on solid libraries written in Java, Scala, Clojure,
or other JVM languages.
* Use the solid platform independent JDBC database
  drivers. Platform dependent drivers used with MRI Ruby are a common
  source of gripe for developers trying to migrate an application from
  one platform to another.

Great prospects indeed! Now it's about time to get that magical piece
of software called JRuby up and running...

## Installing JRuby

There are several options to consider in the department of JRuby
installation. JRuby requires a Java runtime 5.0+ to be installed. You
can get one from [here](http://www.oracle.com/technetwork/java/index.html).

#### Using an Installer

The easiest way to install JRuby is to use one of the prebuilt installers
available from the [official download site](http://jruby.org/download). These will take care of the
low level of detail, such as setting up your **PATH** environment
variable to make finding JRuby easier.
The JRuby team currently maintains installers for Windows and Mac
machines. If you're on Linux, your distribution may package its own
JRuby build. For example, on Ubuntu (or any other Debian derived
distro) you can type this:

``` bash
$ sudo apt-get install jruby
```

Red Had distribution users might try this incantation instead:

``` bash
$ sudo yum install jruby
```

Most Linux distributions don't upgrade to the latest JRuby release the
instant it comes out. If you want to stay with the latest and greatest,
you might prefer installing from an archive instead or RVM instead.

#### Using RVM

Most Ruby hackers
favour a powerful bash script called RVM(Ruby Version Manager) that
allows you to install several different version(or flavours of Ruby)
and switch easily between them. Please refer to the official
[RVM documentation](https://rvm.beginrescueend.com/) for installation
and usage instructions. After you've installed RVM getting JRuby
installed is a child's play:

``` bash
$ rvm list known | grep jruby
jruby-1.2.0
jruby-1.3.1
jruby-1.4.0
jruby-1.6.0
jruby[-1.6.1]
jruby-head

$ rvm install jruby
$ rvm use jruby
```

Just for the record - I personally use RVM and I recommend to all
*BSD, Linux & OS X hackers to try it out as well - great piece of
software. One of the nicer side effects of using RVM is that you won't
have to run operations like **gem install** as the root user.

#### Using prebuilt archive

If you have a heavily customized setup or just like doing things
yourself, you can get a .zip or .tar.gz archive from the same download
page. Extract the archive somewhere convenient on your system, such
as **C:\** or **/opt**. You can run JRuby straight from its own _bin_
folder, but you'll probably find it more convenient to add it to
your PATH. On UNIX (including Linux & Mac OS X), you can do the following:

``` bash
$ export PATH=$PATH:/opt/jruby/bin
```

#### Testing the installation

Type the following commands:

``` bash
$ which jruby
~/.rvm/rubies/jruby-1.6.1/bin/jruby
$ jruby -version
jruby 1.6.1 (ruby-1.8.7-p330) (2011-04-12 85838f6) (Java HotSpot(TM) Server VM 1.6.0_22) [linux-i386-java]
$ jruby -e 'puts "Hello, JRuby!"'
Hello, JRuby!
```

Now we can see some of the unique JRuby features in action.

## Common tasks with JRuby

**REPL**

JRuby comes with an equivalent of the standard Ruby REPL irb, called
jirb. To start it simply type:

``` bash
$ jirb
```

Now you can do some interactive Ruby development:

``` irb
jruby-1.6.1 :001 > puts "Hello, JRuby"
Hello, JRuby
 => nil
jruby-1.6.1 :002 > arr = ["Chuck", "Sarah", "Morgan", "Casey"]
 => ["Chuck", "Sarah", "Morgan", "Casey"]
jruby-1.6.1 :003 > arr.length
 => 4
jruby-1.6.1 :004 > arr.size
 => 4
jruby-1.6.1 :005 > arr.size()
 => 4
jruby-1.6.1 :006 > arr.each { |name| puts name }
Chuck
Sarah
Morgan
Casey
 => ["Chuck", "Sarah", "Morgan", "Casey"]
jruby-1.6.1 :007 > arr.each_with_index { |name, index| puts "##{index}: #{name}"}
0: Chuck
1: Sarah
2: Morgan
3: Casey
 => ["Chuck", "Sarah", "Morgan", "Casey"]
```

jirb is a great tool for exploratory programming and has some nice
features like TAB completion. Use it often!

#### Running scripts

Same as before (with MRI Ruby):

``` bash
$ jruby some_script.rb
```

That was simple, right?

#### Running Ruby tools

You should prefix calls to common Ruby tools like gem and rake with
**jruby -S** - otherwise they might get confused which Ruby version
(if you have more than one Ruby installed, that is) to use:

``` bash
$ jruby -S gem install rails
$ jruby -S rake install
```

#### Using the JRuby compiler

You can compile Ruby scripts directly to Java bytecode and run the
resulting class files using the JVM:

``` bash
$ jrubyc hello.rb
Compiling hello.rb to class example
```

The compiler supplies a main method for you, so you can now run the
program straight from the java command (adjust the path here to point
to your JRuby installation):

``` bash
$ java -cp .:/opt/jruby/lib/hello.jar example
```

Note that your compiled program still depends on some JRuby-defined
support routines, so jruby.jar needs to be on your classpath. Also,
the compiler compiles only the files you specifically pass to it. If
you reference some_ruby_library.rb from hello.rb, you'll have to
compile that extra .rb file yourself or ship it in source form
alongside your .class file. The Java compiler understands dependencies
between source files and compiles them automatically so Java
developers should keep this difference in mind.

## Using Java from JRuby

One of the nicest features of JRuby is undoubtedly the ability to use
Java libraries directly in your Ruby code. JRuby goes a long way to
make the Java classes integrate into normal Ruby code as seamlessly as
possible - for instance it gives you the ability to call methods using the
snake_naming_convention, instead of the common in Java
camelCaseNamingConvention. Let's see the Java integration in action:

``` ruby
require 'java'
java_import 'java.lang.System'
java_import 'java.util.ArrayList'
java_import 'javax.swing.JOptionPane'

System.out.println("Feel the power of JRuby")

## using snake_names for Java method names
puts System.current_time_millis
## regular names work as well
puts System.currentTimeMillis

array_list = ArrayList.new

## the array list supports some common Ruby idioms
array_list << 1
array_list.add 2
array_list << 3

puts "List length is ##{array_list.length}"

array_list.each { |elem| puts elem }

## a glimpse of Swing
JOptionPane.show_message_dialog(nil, "This is a message from the future of Ruby!")
```

You shouldn't, of course, use ArrayList unless you're using a Java API
that is requiring you to do so. Hopefully these simple examples gave
you an idea how easy it is to access Java code from JRuby.

It might be tempting to think of Java/Ruby integration as nothing more
than calling from one language to another. That's not the case. In a
typical project, you're really interacting with both platforms.  You
might construct a Ruby object, pass it to a Java function, and watch
the Java code call other Ruby methods you've defined. All the advanced
interactions are beyond the scope of this cursory overview, but you're
definitely encouraged to explore them on your own.

## Using JRuby from Java

While Java libraries are capable of doing just about anything they are
generally not as elegant as some of their Ruby counterparts. This might
make you want to run some Ruby code from a Java program. JRuby allows
you do this:

``` java
import org.jruby.embed.InvokeFailedException;
import org.jruby.embed.ScriptingContainer;

public class RubyFromJava {
    public static void main(String[] args) {
        ScriptingContainer container = new ScriptingContainer();
        container.runScriptlet("puts 'Ruby bridge established successfully'" );
    }
}
```

This example is quite basic, but you should be able to grasp the basic
idea from it.

## Compatibility with standard Ruby and performance

JRuby 1.6 is mostly compatible with MRI Ruby 1.9.2. Since Ruby doesn't
have a formal standard and is mostly defined in terms of the reference
implementation (although there are some compatibility test suites)
alternative implementations like JRuby are bound to be a step behind
the current reference version from time to time. JRuby, however,
catches up very quickly and has reached a state in popularity and adoption
at which I'm certain that they (the JRuby team) keep an open communication channel with
upstream MRI developers and are capable to add the new features with
very little delay.

In terms of performance JRuby is slightly faster in many tests than
MRI 1.9.2 and with the inclusion of support for dynamic method
dispatching in Java 7 (coming up later this year) the performance will
probably be improved significantly. The only real performance problem
is the JVM startup time. If you're using JRuby to run very simple
scripts you might be mislead to believe that JRuby's very slow, when actually the
delay you're witnessing is caused by the JVM startup (which is not
very fast). Some Ruby features like ObjectSpace don't perform very
well on the JVM as well, but they are used rarely.

In a sentence - JRuby is quite compatible with the standard MRI Ruby
and one of the fastest Ruby implementations around.

## Deployment options and future prospects

With JRuby your number of deployment options vastly improves - now you
can deploy your Ruby applications anywhere where a JVM can be run (and
there are lot such places, believe me about that). With JRuby you can
deploy your Rails applications on the Google App Engine or in a Java
enterprise container such as Glassfish. You can also write mobile
applications for the Android operating system.

JRuby's development is funded by a very solid company, called
["Engine Yard"](http://www.engineyard.com/) which is famous for its world class Rails hosting
solutions. The company obviously has a lot at stake here and you
shouldn't be afraid that JRuby might die anytime soon.

IT consulting companies like
[ThoughtWorks](http://www.thoughtworks.com/) have used JRuby to deliver both products and customer
applications on far more aggressive schedules than they could
have with more conventional languages

## The tools of the trade

Most Ruby hackers tend to program without the aid of sophisticated
IDEs. Emacs, vim and TextMate are popular choices. Recently
[SublimeText](http://www.sublimetext.com/) has been getting a fair share of attention as well. While
it's fairly easy to write Ruby code in a text editor it's generally a
nightmare to write Java code in an editor. Some of the most old-school
hardcore developers that I know bowed down before the complexity of
Java and started using Eclipse, NetBeans or IntelliJ to keep their
sanity intact. When you're working on a project that's a mixture of Ruby
and Java code it might be a good choice to opt for using some IDE as
well.

* [IntelliJ IDEA](http://www.jetbrains.com/idea/) - The legendary Java IDE comes with a very capable
  Ruby plug-in, that integrates well with Rails, the common templating
  languages often used with it and most Ruby testing
  frameworks. IntelliJ even has a variant for pure Ruby development
  called [RubyMine](http://www.jetbrains.com/ruby/) which is regarded by many devs as the best Ruby
  IDE out there.
* [NetBeans](http://wiki.netbeans.org/RubySupport) - At some point the core JRuby team were employed by
  Sun and at that time great Ruby support was added to
  NetBeans. Oracle killed the official Ruby support in NetBeans 7.0,
  but it's still maintained as a community project. It's not as good
  as the one in RubyMine, but it doesn't cost anything either.
* [Eclipse](http://www.eclipse.org/dltk/) - Eclipse has an official
Ruby plug-in(part of DLTK), but most people tend to prefer using
[Aptana Studio](http://www.aptana.com/products/studio3) - a web
development IDE built on top of Eclipse.

## Epilogue

JRuby is a solid addition to the ranks of JVM languages. Given the
fact that Ruby served as the principle inspiration for Groovy many
people will probably do better to use JRuby in preference to Groovy
(except the ones fond of the Java syntax I guess). I personally love
both Ruby and the JVM and for me JRuby was a match made in heaven. It
opens a lot new and exciting possibilities before one of the most
beautiful languages ever conceived.

I particularly like the ability to create portable GUIs with Swing and
the extended deployment options that JRuby provides. If Java 7 brings
the promised speed improvements I'm certain that JRuby will have a
shot at becoming the reigning Ruby implementation.

So what are you waiting for? Go grab a copy of the JRuby Bible
["Using JRuby"](http://pragprog.com/titles/jruby/using-jruby) and
start coding. :-)
