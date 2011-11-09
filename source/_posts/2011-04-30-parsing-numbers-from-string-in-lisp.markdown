---
layout: post
title: "Parsing numbers from string in Common Lisp"
categories:
- Programming
- Common Lisp
---

One task that often recurs in programming is the need to parse a
string representation a number(or several numbers) and convert it to
its numeric value. Parsing integer value in Common Lisp is fairly
straightforward process - we have the built-in function **PARSE-INTEGER**:

``` cl
(parse-integer "100") ;; => 100
(parse-integer "100" :radix 2) ;; => 4
```

As you can see the function allows you to parse a string
representation of a number in an arbitrary base system(the default is
the _decimal_). With the keyword argument **:radix** you can specify a
base in the interval 2-36. The function has a few other fancy
capabilities as well - like the ability to process only a part of the
string that has been passed to it and to ignore junk in the input
string. For all the gory details refer to the
[Lisp HyperSpec](http://www.lispworks.com/documentation/HyperSpec/Body/f_parse_.htm).

The problem that most Lisper face soon after is that there is no
matching function PARSE-FLOAT or PARSE-DOUBLE. I'm not sure what
technical reason is hidden beneath this design decision, but I know of
simple way to parse floating point numbers non-the-less. It's built
around the **READ**(The R in REPL) function that allows you read any
S-expression from a string form. The READ function then returns a Lisp
object corresponding to the S-expression read. With that knowledge and
the fact that READ accepts as an optional argument an input stream
from which to read that S-expression(the default is the the standard
input) we can write the following bit of parsing code:

``` cl
(with-input-from-string (in "3.14")
  (read in))
```

Here we created an input stream that's bound to the string "3.14" and
read one S-expression from it - the floating point object 3.14.

We can even build a more general solution that parses several numbers
in a string, regardless of their actual type(integer or floating
point):

``` cl
(with-input-from-string (in "3.14 5.646 4 9.6")
  (loop for x = (read in nil nil) while x collect x))
;; => (3.14 5.646 4 9.6)
```

Hopefully this short article has been helpful. You've also witnessed
one of the practical benefits of having the code in Lisp represented
as data.
