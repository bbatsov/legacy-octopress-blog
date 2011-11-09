---
layout: post
title: "Java.next() - Clojure: The Return of the Lispers"
categories:
- Clojure
- Java
---

## Prelude

This is the third part of the series of **Java.next()**. Last time
we've discussed the merits of [Scala](/Java/Scala/2011/05/08/jvm-langs-scala.html) - an OO language with a strong
emphasis on functional and parallel programming. Today we'll be
discussing Clojure - a language that pushes the envelop a lot further
than Scala as far as functional and parallel programming are
concerned. You'll see that Clojure is radically different from Scala
and Groovy in many aspects - it's not an OO language, it doesn't have
Algol-derived syntax and it introduces a few rather radical ideas on
subjects such as [identity and state](http://clojure.org/state).

Clojure's approach to concurrency is characterized by the concept of
identities, which represent a series of immutable states over
time. Since states are immutable values, any number of workers can
operate on them in parallel, and concurrency becomes a question of
managing changes from one state to another. For this purpose, Clojure
provides several mutable reference types, each having well-defined
semantics for the transition between states. This is a pretty complex
topic for a language overview so I'll discuss it here only cursory.

Clojure was initially conceived as targeting both the JVM and the
CLR. For various reason currently the core development team is targeting mainly
the JVM and the [CLR port](https://github.com/richhickey/clojure-clr)
is receiving less attention (though it's not abandoned and it's
regularly being updated). Like Scala it's not technically correct to
call it a JVM languages, because it's both a JVM and a .Net language,
but since it's used a lot more often with Java it doesn't make that
much of a difference.

## A brief history of Clojure

Clojure is a very young project (compared to most popular
programming languages at least). It was created in 2007 by Rich
Hickey (project leader and benevolent dictator for life). He developed
Clojure because he wanted a modern Lisp for functional programming,
symbiotic with the established Java platform, and designed for
concurrency. What started as a hobby project turned into some much
bigger with Rich getting so excited about the project that left his
job to work full-time on the project, effectively through burning his life's
savings in the process. This was quite the gamble, but it turned out
to be a lucky one, since Clojure's popularity rapidly spiked and
loyal and energetic community was quickly formed around the project.

Clojure became the new language of choice for many well respected
hackers from different communities. I've noticed something of a trend
in that department - most Clojure hackers used to be Ruby hackers. I
guess some of the Ruby hackers were not satisfied by partial subset of
Lisp features, available in Ruby, and wanted to gain access to all of
Lisp's power.

The current Clojure version is 1.2 with 1.3 being just around the
corner.

## Installing Clojure

_Before installing Clojure make sure you have Java installed. Java 5.0
SE will do, but Java 6 SE is highly recommended._

Installing Clojure is just a matter of downloading and extracting a
single archive -
[clojure.zip](http://github.com/downloads/clojure/clojure/clojure-1.2.0.zip). Many
high quality Clojure libraries come prepackaged in another archived
named
[Clojure Contrib](http://github.com/downloads/clojure/clojure-contrib/clojure-contrib-1.2.0.zip). Clojure
Contrib is kind of a staging area for Clojure development - it's a
common practice to move some of the best parts of contrib into core.

In the directory in which you expanded clojure.zip, run:

``` bash
$ java -cp clojure.jar clojure.main
```

This will bring up a simple read-eval-print loop (REPL) a.k.a. an
interactive console. Much of
Clojure is defined in Clojure itself (in the **core.clj** file included in
the src directory of distribution), which is automatically loaded from
the .jar file when Clojure starts. The file **user.clj**, if found in the
classpath, will be auto-loaded as well. You can leverage this to cause
code to run when Clojure starts. Reading the code in core.clj is a
very good way to get started with language and see how real Clojure
hackers work.

When core.clj is loaded you will have the language as described herein fully available.
Try:

``` clojure
user=> (+ 1 2 3)
6
user=> (println "Hello, Clojure!")
Hello, Clojure!
nil
user=> (javax.swing.JOptionPane/showMessageDialog nil "Hello World")
```

The REPL has very rudimentary editing. For a better experience, try running it via the [JLine](http://jline.sourceforge.net/) ConsoleRunner:

``` bash
java -cp jline-0_9_5.jar:clojure.jar jline.ConsoleRunner clojure.main
```

This will give you left/right arrow key navigation and up/down arrow
command history.

Later on we'll see how to setup a real Clojure development environment
in which you'll be able to leverage the full power of the Clojure REPL
and interactive programming.

## Did you say Clojure was a Lisp???

Most developers tend to have a very negative attitude towards the word
**Lisp** in general. I guess it spawns all kinds of nasty associations in
their brains - like prefix syntax notation, tons of parentheses and a
lot of crap they heard about Lisp from their 70 year-old professor,
teaching introduction to functional programming in college, whose
notion of functional programming is that in Lisp everything is a
function (believe me when I tell you this - such professors do exist).

You know, I wasn't born coding in Lisp myself. I was initially
exposed to Lisp when I tried to learn the Emacs text editor and I was
baffled by many things - the strange syntax, the talk about atoms and
lists, code as data, macros, continuation, tail-call optimizations,
what to quote and that to evaluate, what is a s-expression and what
isa form. To put it shortly - I was like
Alice down the rabbit whole or like Neo when he found out what the
Matrix is... The world of programming that I was familiar with was
turned upside down.

The interesting thing is that I felt similarly when I learnt my first
programming language Pascal in the 8th grade. It's not that Lisp is
any harder than the other programming languages - it's just that it's
different and you're usually approaching it from a position in which
you know one or several programming languages, using the much more
widespread Algol syntax. I advise you to simply keep an open mind while
you read this article and don't just dismiss Clojure because of its
Lisp heritage.

You likely know at least one person who constantly keeps telling
you how Lisp is the one true programming language, how everything
pales next to it and how Lisp is the actual answer to that fundamental
question about the life, the universe and everything else (not
42). These people might very well be telling the truth, but their
zealous rants tend to create a negative attitude towards the Lisp
community as well. Please, ignore them.

Now it's time to take the red pill... So fasten your seat-belt
Dorothy, 'cause Kansas is going bye-bye!

## Clojure at a glance

{% blockquote Rich Hickey, creator of Clojure %}
Mutable state is the new spaghetti code!
{% endblockquote %}

{% blockquote Rich Hickey, creator of Clojure %}
Time is the new memory!
{% endblockquote %}

{% blockquote Stuart Halloway, author of "Programming Clojure" %}
Clojure feels like a general-purpose language beamed back from the
near future. Its support for functional programming and software
transactional memory is well beyond current practice and is well
suited for multicore hardware. At the same time, Clojure is well
grounded in the past and the present. It brings together Lisp and the
Java Virtual Machine. Lisp brings wisdom spanning most of the history
of programming, and Java brings the robustness, extensive libraries,
and tooling of the dominant platform available today.
{% endblockquote %}

If I had only a few minutes to describe Clojure this would be the gist
of it:

* Dynamic language for the JVM
    * Clojure uses dynamic typing like languages such Ruby and Python
      and a very smart compiler that will generally generate very
      efficient bytecode. If you want to push the performance envelope even
      further you can add some explicit type hints in your Clojure
      code to ensure the generation of even faster bytecode.
* Lisp reloaded
    * Clojure is Lisp down to its core - it has all the features that
      are known and loved, and in the same time it improves upon them in
      several ways - for instance we have a literal syntax for most
      common collection types. Sure - with Common Lisp's reader macros
      one can do this as well, but nobody bothers to...
* Elegant
    * Clojure code tends to be very concise, but very readable non the
      less. A core idea in Clojure is to strip the incidental
      complexity of problems solving and to be able to just solve the
      problems straight away without much ceremony.
* Functional
    * Clojure puts heavy emphasis on functional programming, but it's
      a practical functional programming language - not a pure one
      like Haskell. Clojure acknowledges that some stuff simply change
      and operations have to generally produce some effects, and makes
      those things easy to model. Clojure has a library full of
      rock-solid immutable data structures, relies heavily on lazy
      evaluation, tail-recursion and higher-order functions.
* Designed with concurrency in mind
    * Clojure has an extensive built-in high-level facilities to deal
      with concurrent access to data and parallel programming in general.
* Fast
    * Unlike many dynamic languages (even those running on top the
      JVM) Clojure is quite fast - it some scenarios it's performance
      can rival that of a statically type language. You can browse a
      long list of
      [benchmark comparisons](http://stackoverflow.com/questions/2186709/are-there-any-good-clojure-benchmarks)
      to verify this statement. Given the fact that performance if
      often cited as a big drawback of dynamic languages, this is
      quite the win for Clojure.
* Capable of easily leveraging existing Java code
    * Using Java code from Clojure is direct, easy and
      idiomatic. There are no intermediate layers or the need to
      write wrapper for everything.

I'll discuss in greater detail some of those features as I moving along.

## A whirlwind tour of Clojure

#### Clojure is elegant

* Removes a lot of accidental complexity
* Clojure programs are generally expressive and concise
* Concise programs are naturally easier to understand and maintain

Consider this Java example from our Scala discussion:

``` clojure
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

As a reader pointed out using the third party Guava library the code
can be reduced to:

``` clojure
public boolean hasUpperCase(String word) {
    if (null != word)
        return any(charactersOf(word), new Predicate() {
                public boolean apply(Character c) {
                    return isUpperCase(c);
                }
            })
        else
            return false;
}
```

It still looks quite ugly to me. For the sake of comparison here's the
Clojure version:

``` clojure
(defn has-uppercase? [string]
  (some #(Character/isUpperCase %) string))
```

The definition of the problems is "A string has an uppercase character if
some of the characters in it is uppercase" (doesn't sound good, but
will do). The Clojure code reads more or less like the definition of
the problem. A finer point is that it will work correctly even if you
pass **nil** to the has-uppercase? function.

#### Clojure is concise

We already saw in the previous example the conciseness of Clojure
code, but here we'll add another example. This is Java:

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

In Clojure you'd probably model this class like this:

``` clojure
user> (defrecord person [name age])
user.person
user> (person. "Bozhidar" 26)
#:user.person{:name "Bozhidar", :age 26}
user> (def me (person. "Bozhidar" 26))
#'user/me
user> (:name me)
"Bozhidar"
user> (:age me)
26
```

Clojure's version of the type is a one liner and remain shorter even
with a few examples of its usage. It's not equivalent to Java
definition, however - the Clojure version of the structure is
immutable.

#### Clojure is a Lisp

For better or for worse Clojure is a Lisp dialect and we should accept
this. I have always viewed Lisp as weapon from a more elegant era when
people were more concerned with elements of style and empowering the
developers to easily translate their thoughts into programs. For one
reason or another every Lisp dialect has failed to capture the
attention of a critical mass of developers that may propel it into the
mainstream. This, of course, doesn't mean that existing Lisp dialects
should be considered a failure. Scheme (the dialect that has probably
had the greatest impact on Clojure's design) was designed to be as
simple as possible so it could be appropriate as a teaching tool - in
that area Scheme certainly excelled. Common Lisp was created to bring
together the various Lisp dialects under a common denominator and it
also excelled in that endeavour. I guess that its creators hoped that
it would capture a significant market share at some point as well, but alas -
that never happened.

The syntax and programming model of Lisp so far have been too much for
a typical developer to absorb. Yet, there’s something special about
Lisp that’s worth revisiting, so the new dialects continue to
emerge. Some of the best programming universities start teaching
programming with the Lisp language to form young minds while they are
still open. I have witnessed something of a cycle - every 5 or so
years the interest in Lisp spikes because of something major that
happened in the land of Lisp. In the beginning of the nineties the
work on Common Lisp excited a lot of developers. Five years later Paul
Graham took the stage - he showed the world how Lisp can empower small
teams and make real money (if you haven't heard of Viaweb fire up
google now). Five years ago Peter Seibel published the
"Practical Common Lisp" book that appeared on Amazon's bestseller list
and got a lot of new developers excited about Lisp. A now... well I
guess you can figure that one out on your own.

Lisp just won't let go and die. There is something magical about
it. And there is this inexplicable smugness on the face of Lisp
developers...

So let's review the typical Lisp features that are present in Clojure:

* Lisp-1 dialect
    * This means that functions and variables share the same
      namespace, unlike in dialects like Common Lisp. Both approaches
      have their merits and drawbacks as usual. In Clojure you cannot
      have a variable named the say way as a function, but you can
      pass function names around without any special syntax. In Common
      Lisp you can have function and variables sharing the same name,
      but you have to mark functions explicitly when you're passing
      them around (with the #' reader macro or the **function** function).
* Dynamic - both in term of dynamic typing and dynamic
  development. Lisp is the language that made popular the technique of
  incremental interactive development (we'll talk about it more in a bit)
* Code is data
    * List code is defined in term of Lisp data structures. When the
      reader read the source code of the application it converts it to
      standard Lisp objects and they represent the program. No special
      transformations, no AST. This is the heart of Lisp macros and a
      centrepiece in Lisp philosophy.
* Reader
    * The reader can read valid Clojure forms and translate them into
      Clojure objects - object, function call, everything that has a
      readable representation
* Small core, next to none syntax
    * In terms of compact syntax and uniformity of the syntax it has
      always been hard to beat Lisp. Most programming languages are
      full of special syntax constructs, keywords, etc. In lisp
      programs are just lists and the low-level plumbing comes in the
      form of special functions called special forms. Everything else
      is implemented in terms of those special forms.
* Sequences
    * Clojure abstracts common collection traits into an abstraction
      called seq which allows you to use a similar API for many tasks
* Macros
    * Forget about C macros, Word macros, editor macros. Lisp macros
      are the most powerful metaprogramming technique out there - they
      enable you generate new syntax abstractions unlike anything
      else. If you need a new operator in Java you'd have a hard time
      convincing the guys in Oracle to add it for you. With Lisp
      you're in charge and you can define any syntax abstractions that
      you wish. As an appetiser consider the **and** boolean
      statement. In most languages it's built into the language
      itself. In Clojure it's just a short macro:

``` clojure
(defmacro and
  "Evaluates exprs one at a time, from left to right. If a form
  returns logical false (nil or false), and returns that value and
  doesn't evaluate any of the other expressions, otherwise it returns
  the value of the last expr. (and) returns true."
  {:added "1.0"}
  ([] true)
  ([x] x)
  ([x & next]
   `(let [and# ~x]
      (if and# (and ~@next) and#))))
```

I hope this example gives you an idea about the power that Clojure
offers you - you can be more than just a programmer; you can be the
language designer.

## Persistent data structures

Data structures in Clojure are immutable. Operations executed on them
return a new data structure of the same type instead of modifying the
structure in place. Understandably most people are immediately
concerned about the performance implications of such a technique -
this seems like quite a lot of overhead. They needn't worry, though.

Data structures in Clojure happen to be persistent as well. A persistent data
structure is a data structure which always preserves the previous
version of itself when it is modified -  such data structures are
effectively immutable, as their operations do not (visibly) update the
structure in-place, but instead always yield a new updated
structure. A persistent data structure is not a data structure
committed to persistent storage, such as a disk; this is a different
and unrelated sense of the word "persistent".

Persistent data structures save a lot of copying around and improve
greatly the performance. Knowing this should be enough for most
developers, those that are more curious can find a lot of interesting
articles on the subject on-line.

The core data structures in Clojure are:

* List
* Set - all the items in it are unique
* Map - also known as associative array and dictionary in other languages
* Vector - also know as one dimensional array

Let's see them in action:

``` clojure
;;; Lists
;; list creation
user> (list 1 2 3)
(1 2 3)
;; quoted list creation
user> (def a-list '(1 2 3 4 5 6 7 8 9 10))
#'user/a-list
;; find the size of a list
user> (count a-list)
10
user> (first a-list)
1
user> (rest a-list)
(2 3 4 5 6 7 8 9 10)
user> (last a-list)
10
;; find the elements of the list matching a predicate(boolean function)
user> (filter even? a-list)
(2 4 6 8 10)
user> (filter odd? a-list)
(1 3 5 7 9)
;; map an anonymous(lambda) function to all elements of the list
user> (map #(* % 2) a-list)
(2 4 6 8 10 12 14 16 18 20)
;; add an element to the beginning of the list
user> (cons 0 a-list)
(0 1 2 3 4 5 6 7 8 9 10)
;; cons in a list specific function, conj is a general purpose one and
;; works on all collection (but in a different manner)
user> (conj a-list 0)
(0 1 2 3 4 5 6 7 8 9 10)
;; retrieve the first five items in a list
user> (take 5 a-list)
(1 2 3 4 5)
;; retrieve all but the first five items in a list
user> (drop 5 a-list)
(6 7 8 9 10)
user> (take-while #(< % 3) a-list)
(1 2)
user> (drop-while #(> % 3) a-list)
(1 2 3 4 5 6 7 8 9 10)
user> (drop-while #(< % 3) a-list)
(3 4 5 6 7 8 9 10)

;;; Sets

user> (set '(1 2 3 4 5 1 2 3 4))
#{1 2 3 4 5}
user> (def a-set #{1 2 3 4 5})
#'user/a-set
user> (contains? a-set 3)
true
user> (contains? a-set 7)
false
user> (conj a-set 5)
#{1 2 3 4 5}
user> (conj a-set 6)
#{1 2 3 4 5 6}
user> (disj a-set 1)
#{2 3 4 5}
user> (get a-set 1)
1
user> (get a-set 7)
nil
;; most set functions live in the clojure.set namespace
user> (use 'clojure.set)
nil
user> (difference #{1 2 3} #{1 3 5})
#{2}
user> (intersection #{1 2 3} #{1 3 5})
#{1 3}
user> (union #{1 2 3} #{1 3 5})
#{1 2 3 5}

;;; Maps
user> (hash-map :Bozhidar :Batsov :Bruce :Wayne :Selina :Kyle)
{:Selina :Kyle, :Bozhidar :Batsov, :Bruce :Wayne}
user> (def a-map {:Bozhidar :Batsov, :Bruce :Wayne, :Selina :Kyle})
#'user/a-map
user> a-map
{:Bozhidar :Batsov, :Bruce :Wayne, :Selina :Kyle}
user> (get a-map :Bozhidar)
:Batsov
user> (contains? a-map :Bozhidar)
true
user> (contains? a-map :Clark)
false
user> (:Bozhidar a-map)
:Batsov
user> (assoc a-map :Lois :Lane)
{:Lois :Lane, :Bozhidar :Batsov, :Bruce :Wayne, :Selina :Kyle}
user> (keys a-map)
(:Bozhidar :Bruce :Selina)
user> (vals a-map)
(:Batsov :Wayne :Kyle)
user> (dissoc a-map :Bruce)
{:Bozhidar :Batsov, :Selina :Kyle}
user> (merge a-map {:Alia :Atreides, :Arya :Stark})
{:Arya :Stark, :Alia :Atreides, :Bozhidar :Batsov, :Bruce :Wayne, :Selina :Kyle}

;;; Vectors

user> (vector 1 2 3 4)
[1 2 3 4]
user> [1 2 3 4]
[1 2 3 4]
user> (def a-vector [1 2 3 4 5])
#'user/a-vector
user> (count a-vector)
5
user> (conj a-vector 13)
[1 2 3 4 5 13]
;; random access is a constant time operation in vectors
user> (nth a-vector 3)
4
user> (pop a-vector)
[1 2 3 4]
user> (peek a-vector)
5
```

Most data structures in Clojure are part of a common Sequence API,
that we'll briefly discuss shortly.

## The Seq API

Clojure defines many algorithms in terms of sequences (seqs). A seq is
a logical list, and unlike most Lisps where the list is represented by
a concrete, 2-slot structure, Clojure uses the ISeq interface to allow
many data structures to provide access to their elements as
sequences. The **seq** function yields an implementation of ISeq
appropriate to the collection. Seqs differ from iterators in that they
are persistent and immutable, not stateful cursors into a
collection. As such, they are useful for much more than foreach -
functions can consume and produce seqs, they are thread safe, they can
share structure, etc.

Most of the sequence library functions are lazy, i.e. functions that
return seqs do so incrementally, as they are consumed, and thus
consume any seq arguments incrementally as well. Functions returning
lazy seqs can be implemented using the **lazy-seq** macro. The laziness
allows us to deal with infinite data structures easily (as long as we
don't try to act on all of their elements that is):

{% highlight clojure %}
user> (take 10 (filter even? (iterate inc 1)))
(2 4 6 8 10 12 14 16 18 20)
{% endhighlight %}

**iterate** returns an infinite lazy sequence. **filter** returns a lazy
sequence as well. With **take** we can take only the elements we need
without have to process the entire infinite collection.

## Functional programing with Clojure

Clojure is a functional programming language and as such it offers quite
the selection of features that make it easy to leverage the functional
programming techniques.

* functions are objects
* all built-in data structures are immutable
* most functions in the core library are pure (they don't produce any
  side results and they don't interact with the outside world in any
  manner other than just receiving their parameters from it)
* there are no iteration constructs like **for** and **while** in
  other languages. In place of iteration list comprehensions and
  recursion are commonly used.
* everything is an expression that yields some result - even things
  that are traditionally statements in other languages such as **if** and
  **print** (although the return value of print is not particularly useful)

## Parallel programming

Functional programming and parallel programming complement each
other. When most of your code is contained in pure functions it's
naturally tread safe (not to mention much easier to test). Since you
don't have any mutable state there, it's absolutely safe to fire those
pure functions in as many threads as you wish and you'll have
absolutely nothing to worry about.

Programs, however, eventually produce side effects and often they
really have to have some mutable state. Clojure makes it easy to model
such situations in your programs in a way that doesn't compromise the
ability to parallelize the programs.

#### Refs and transactions

Transactional references (known as refs in Clojure) ensure safe shared use of mutable
storage locations via a software transactional memory (STM)
system. Refs are bound to a single storage location for their
lifetime, and only allow mutation of that location to occur within a
transaction.

Clojure transactions should be easy to understand if you've ever used
database transactions - they ensure that all actions on refs are
atomic, consistent, and isolated. Atomic means that every change to
refs made within a transaction occurs or none do. Consistent means
that each new value can be checked with a validator function before
allowing the transaction to commit. Isolated means that no transaction
sees the effects of any other transaction while it is running. Another
feature common to STMs is that, should a transaction have a conflict
while running, it is automatically retried.

There are many ways to do STMs (locking/pessimistic,
lock-free/optimistic and hybrids) and it is still a research
problem. The Clojure STM uses multiversion concurrency control with
adaptive history queues for snapshot isolation, and provides a
distinct commute operation. Here's a short example:

``` clojure
(def picked-numbers (ref #{})

(def secret-num (.nextInt (java.util.Random.) 10))

(defn guess-number [n]
        (print "Enter a guess between 1 and 10: ")
        (flush)
        (let [guess (java.lang.Integer/parseInt (read-line)) ]
             (cond
               (= guess n) (println "You guessed correctly")
               (contains? (deref picked-numbers) n) (println "Pick another number! You already tried that one.")
               :else (dosync
                      (alter picked-numbers conj guess)))))

user=> (guess-number secret-num)
Enter a guess between 1 and 10: 1
#{1}
user=> (guess-number secret-num)
Enter a guess between 1 and 10: 3
#{1 3}
user=> (guess-number secret-num)
Enter a guess between 1 and 10: 5
#{1 3 5}
```

I hope you got the basic idea from this simple, but mostly useless
snippet. Generally when we have only one object that we'll be changing
in this manner an atom is a more appropriate choice as we'll see shortly.

#### Agents

Like _refs_, _agents_ provide shared access to mutable state. Where refs
support coordinated, synchronous change of multiple locations, agents
provide independent, asynchronous change of individual
locations (to put it into simpler term you'd use refs if you had to
updated several things and wait for the update to happen and agents if
you need to update only one thing and don't really care when the
update will happen - only that it will happen). Agents are bound to a single storage location for their
lifetime, and only allow mutation of that location (to a new state) to
occur as a result of an action. Actions are functions (with,
optionally, additional arguments) that are asynchronously applied to
an agent's state and whose return value becomes the agent's new
state. Let's see an agent (Smith maybe?) in action:

{% highlight clojure %}
user> (def some-agent (agent 0))
#'user/some-agent
user> (dotimes [i 100]
               (send some-agent inc))
nil
user> some-agent
#<Agent@15c024c: 100>
user> @some-agent
100
{% endhighlight %}

#### Atoms

Atoms provide a way to manage shared, synchronous, independent
state. They are a reference type like refs and vars. You create an
atom with atom, and can access its state with deref (or @). Let's
rework the refs example to use an atom:

``` clojure
(def picked-numbers (atom #{})

(def secret-num (.nextInt (java.util.Random.) 10))

(defn guess-number [n]
        (print "Enter a guess between 1 and 10: ")
        (flush)
        (let [guess (java.lang.Integer/parseInt (read-line)) ]
             (cond
               (= guess n) (println "You guessed correctly")
               (contains? (deref picked-numbers) n) (println "Pick another number! You already tried that one.")
               :else (swap! picked-numbers conj guess))))

user=> (guess-number secret-num)
Enter a guess between 1 and 10: 1
#{1}
user=> (guess-number secret-num)
Enter a guess between 1 and 10: 3
#{1 3}
user=> (guess-number secret-num)
Enter a guess between 1 and 10: 5
#{1 3 5}
```

#### Vars

Bindings created with the **binding** macro cannot be seen by any other
thread. Bindings created with binding can be assigned to, which
provides a means for a nested context to communicate with code before
it on the call stack.

I'll not be discussing them further, because Vars are a vast subject
deserving its own post.

## OOP, Lisp style

Object oriented programming in most programming languages is based on
a single dispatch message passing. The object on which we invoke a
method (poor choice of words, but easier to comprehend) is the
receiver, the method name and it's arguments are the message. The
method's invoked solely on the base of the type of the receiver
object.

Lisps have traditionally implemented OOP with generic methods, that
don't have a receiver and are dispatched on the basis of the types of
all of their arguments. In the world of multiple dispatch the more
traditional single dispatch is just a special case in which only the
type of the first method argument matters. Here's a taste of
multimethods in Clojure:

``` clojure
(defmulti my-add (fn [x y] (and (string? x) (string? y))))

(defmethod my-add true [x y]
    (str x y))

(defmethod my-add false [x y]
    (+ x y))

user=> (my-add 3 4) ; => 7
user=> (my-add "3" "4") ; => "34"
```

Here we defined a multi-method that behaves differently for string and
numeric arguments - strings args are concatenated and numeric args are
added together.

## Interactive development

Traditional programming languages have more or less the following work
flow:

* write the unit tests (power to TDD)
* write the source file
* compile the source file (if needed)
* run the source file with an interpreter or run the binary file that
  resulted from the compilation step
* if you need to modify something you edit the code and repeat the
  other steps

Those programs naturally have some entry points. Alternative you can
simple use the test suite you've initially developed.

A Lisp developers generally has a very different work flow:

* start a REPL
* write some unit tests
* write a few functions definitions in a source file
* compile them interactively and load them in a REPL
* test these functions directly from the REPL
* if you need to modify a function - just edit it and reload in the
  REPL

I've been a C/C++ and Java developer for a long time and I didn't see
anything wrong with first model. In fact - I had been practising it
for so very long that it felt quite natural to me. After I've started
hacking with Lisp, however, my old work flow started to feel very
unproductive to me (especially with statically typed languages). Here
are some key aspects of the interactive (and iterative) development
that is so common in Lisp (not only in Common Lisp ;-) ):

* The REPL is an integral process of the coding process. Ruby and
  Python developers generally tend to use it only for exploratory
  programming although many of the techniques common for Lisp could be
  applied for Ruby and Python as well.
* Functions can be defined (and redefined) in real time
* Loading & compilation of code at runtime
* Powerful introspection features
* Interactive development
* Iterative development - you know the old saying "Lather, rinse,
  repeat..." (probably one of the oldest examples of recursion).

## The tools of the trade

The single biggest problem with Clojure in the moment (at least in my
opinion) has nothing to do with the language itself. The problem is
the lack of decent tooling and infrastructure around it. Lisp hackers
have traditionally favoured the SLIME development environment for
Emacs. Unfortunately the maintainers are not especially interested in
having Clojure support (since SLIME targets Common Lisp) and nobody in
Clojure community seems to be capable of writing an adequate swank
component for Clojure that can be used with an up-to-date version of
SLIME. The existing one is quite rudimentary and doesn't work with
stock SLIME distributions. But this is not the worst part - the worst
part is that even this crippled SLIME is still the best development
tool for Clojure. IntelliJ's plug-in is almost unusable, Eclipse's is
barely usable and NetBeans's cannot be installed half the time...

* IDEs
   * [IntelliJ IDEA](http://plugins.intellij.net/plugin/?id=4050) -
     everyone knows how much I love IntelliJ IDEA. Sadly I cannot say
     a good word about the La Clojure plug-in. Its mostly unmaintained
     (and often broken), has pretty limited features and is generally
     good for... nothing. It's sad to see it's so far back in
     JetBrains's priority list - they are doing wonderful things in
     their Groovy and Scala plugins.
   * [Eclipse](http://code.google.com/p/counterclockwise/) - Eclipse
     certainly boasts the best IDE Clojure plug-in at the moment (Counter
     clock-wise). It has a lot of features found otherwise only in
     SLIME. It even features partial paredit support. Being the best
     in such a sorry bunch is not quite an achievement, but at least
     the guys there are trying really hard and I'm sure that within one
     or two releases they'll have a great product.
   * [NetBeans](http://www.enclojure.org/) - The Enclojure plug-in
     seems to be abandoned currently. It has no released a new version
     in over an year and the old one were buggy as hell (when they the
     decency to get themselves installed, that is).
   * [SLIME](https://github.com/technomancy/swank-clojure) - The Ultimate Clojure programming environment. Even though
     it's lacking a few features of the Common Lisp counterpart, SLIME
     still is the best option for Clojure development, uniquely
     attuned to the Lisp philosophy of interactive and incremental development.

Luckily there's no lack of good build tools that one can use with Clojure.

* Build tools
   * [Apache Maven](http://maven.Apache.org) - Maven has a nice
     Clojure plugin
   * [Leiningen](https://github.com/technomancy/leiningen) - probably
     the most popular Clojure-specific build tool
   * [Cake](https://github.com/ninjudd/cake) - a solid alternative to Leiningen
   * [Gradle](http://www.gradle.org/) - a build system for Java-based
     applications, written in Groovy, that supports Clojure
   * [Apache Builder](http://buildr.apache.org/) - a build system for
     Java-based applications, written in Ruby , that supports Clojure

## Resources

* Books
   * ["Programming Clojure"](http://pragprog.com/titles/shcloj/programming-clojure)
   * ["Practical Clojure"](http://www.apress.com/9781430272311)
   * ["The Joy of Clojure"](http://joyofclojure.com/)
* Screencasts & Video lectures
   * ["Clojure's channel"](http://clojure.blip.tv/)
* Websites & Blogs
   * [Official website](http://blog.fogus.me/)
   * [Disclojure](http://disclojure.org/) - a clojure news aggregator
* Exercises
   * [Lisp problems](/blog/2011/05/04/lisp-problems/) - a work in progress, I'll add Clojure
     solutions next to the Common Lisp ones when I have some thime
   * [Labrepl](http://foognostic.net/labrepl-summary/)
   * [Project Euler](http://projecteuler.net/)
   * [Clojure Koans](https://github.com/functional-koans/clojure-koans)

## Epilogue

Clojure is a radical departure from both traditional Algol-derived
languages and existing Lisp dialects. Its advanced support for
functional programming, combined with a state of the art concurrency
support make it attractive language for the development of heavy duty
enterprise grade systems. Coupled with the seamless Java integration
the sky seems to be the limit for Clojure...

Unfortunately Clojure has to face several problems if it's to
succeed. First of all it has to attract a critical mass of developers
that are not afraid of the syntactic difference with common
languages. Then there is the concept of functional thinking - a way of
thinking quite foreign to most developers. To be able to properly
leverage the full power of Clojure developers have to be ready to
overcome a steep learning curve, but rest assured, the prize at the
end of the journey is well worth it.

Another gripe with Clojure at this point is the lack of decent
tooling. Sure, we have the *supported* SLIME, available in ELPA, but
even Emacs users are not particularly happy with it. And let's face
reality - it's quite unlikely that many developers will be willing to
give up the comfort of their beloved IDEs just to be able to code in
Clojure. Eclipse, IntelliJ & NetBeans are unfortunately nowhere near
providing a good Clojure experience. Hopefully, this will change
soon...

I'm a very big fan of Lisp in general, that is no secret. I've tried
to be as objective as possible and abstained myself from over
extolling some of Clojure's virtues. I'd like to say, however, that
I'm very excited that we finally have a Lisp dialect that is modern,
simple, powerful, elegant and most of all - capable of getting the job
done. I really hope that Clojure will be instrument of Lisp return on
the centre stage of programming, where it deserves to be.

As usual the article is very shallow overview and doesn't even
mention some important features of the language. Be sure to check out
some of the resources mentioned.

_P.S. This is the last of the articles that I'd originally intended to
write. I'm considering the possibility to write a couple of more
chapter of the Java.next() series if people are interested to read
them. JRuby will probably make an appearance, but I'd like to hear
some reader input as well. So, what JVM language do you think is
worthy enough to make an appearance in the Java.next() series?_
