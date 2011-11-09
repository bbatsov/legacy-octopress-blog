---
layout: post
title: "Lisp Problems"
categories:
- Misc
- Common Lisp
---

## Prelude
This is a remake of the P-99: Ninety-Nine Prolog Problems collection
that Werner Hett assembled over several years of teaching at the University of
Applied Sciences (Berner Fachhochschule) at Biel-Bienne,
Switzerland. The collection is structured into seven sections. I have
renumbered the problems in order to get more freedom to rearrange
things within the sections.

The purpose of this problem collection is to give you the opportunity
to practice your skills in logic programming. Your goal should be to
find the most elegant solution of the given problems. Efficiency is
important, but logical clarity is even more crucial. Some of the
(easy) problems can be trivially solved using built-in
functions. However, in these cases, you learn more if you try to find
your own solution.

The problems have different levels of difficulty. Those marked with a
single asterisk (\*) are easy. If you have successfully solved the
preceeding problems you should be able to solve them within a few (say
15) minutes. Problems marked with two asterisks (\*\*) are of
intermediate difficulty. If you are a skilled Prolog programmer it
shouldn't take you more than 30-90 minutes to solve them. Problems
marked with three asterisks (\*\*\*) are more difficult. You may need
more time (i.e. a few hours or more) to find a good solution.

## Lisp Lists
---

**1.01 (\*) Find the last element of a list.**

_Do not use the built-in LAST function._

``` cl
CL-USER> (my-last '(1 2 3))
3
```

[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p101.lisp)

**1.02 (\*) Find the penultimate(last but one) element of a list.**

_Do not use a combination of LAST and BUTLAST._

``` cl
CL-USER> (penultimate '(1 2 3))
2
```
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p102.lisp)

**1.03 (\*) Find the nth element of a list.**

_Do not use the built-in function NTH. The first element in the list is number 0._

``` cl
CL-USER> (my-nth '(1 2 3) 1)
2
```

[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p103.lisp)

**1.04 (\*) Find the number of elements of a list.**

_Do not use the built-in function LENGTH._

``` cl
CL-USER> (my-length '(1 2 3))
3
```

[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p104.lisp)

**1.05 (\*) Reverse a list.**

_Do not use the built-in function REVERSE._

``` cl
CL-USER> (my-reverse '(1 2 3))
(3 2 1)
```

[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p105.lisp)

**1.06 (\*) Find out whether a list is a palindrome.**

_A palindrome can be read forward or backward; e.g. (1 2 3 2 1)._

{% highlight cl %}
CL-USER> (palindrome-p '(1 2 3))
NIL
CL-USER> (palindrome-p '(1 2 3 2 1))
T
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p106.lisp)

**1.07 (\*\*) Flatten a nested list structure.**

_Transform a list, possibly holding lists as elements into a 'flat'
list by replacing each list with its elements (recursively)._

{% highlight cl %}
CL-USER> (flatten '(a (b c) ((d e) f)))
(a b c d e f)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p107.lisp)

**1.08 (\*\*) Eliminate consecutive duplicates of list elements.**

_If a list contains repeated elements they should be replaced with a
single copy of the element. The order of the elements should not be
changed._

{% highlight cl %}
CL-USER> (compress '(a a a a b c c a a d e e e e))
(a b c a d e)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p108.lisp)

**1.09 (\*\*) Pack consecutive duplicates of list elements into sublists.**

_If a list contains repeated elements they should be placed in
separate sublists._

{% highlight cl %}
CL-USER> (pack '(a a a a b c c a a d e e e e))
((a a a a) (b) (c c) (a a) (d) (e e e e))
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p109.lisp)

**1.10 (\*) Run-length encoding of a list.**

_Use the result of problem 1.09 to implement the so-called run-length
encoding data compression method. Consecutive duplicates of elements
are encoded as terms [N,E] where N is the number of duplicates of the
element E._

{% highlight cl %}
CL-USER> (encode '(a a a a b c c a a d e e e e))
((4 a) (1 b) (2 c) (2 a) (1 d) (4 e))
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p110.lisp)

**1.11 (\*) Modified run-length encoding.**

_Modify the result of problem 1.10 in such a way that if an element has
no duplicates it is simply copied into the result list. Only elements
with duplicates are transferred as (number element) terms._

{% highlight cl %}
CL-USER> (encode-modified '(a a a a b c c a a d e e e e))
((4 a) b (2 c) (2 a) d (4 e))
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p111.lisp)

**1.12 (\*\*) Decode a run-length encoded list.**

_Given a run-length code list generated as specified in problem
1.11. Construct its uncompressed version._

{% highlight cl %}
CL-USER>
(decode '((4 a) b (2 c) (2 a) d (4 e)))
(a a a a b c c a a d e e e e)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p112.lisp)

**1.13 (\*\*) Run-length encoding of a list (direct solution).**

_Implement the so-called run-length encoding data compression method
directly. I.e. don't explicitly create the sublists containing the
duplicates, as in problem 1.09, but only count them. As in problem
1.11, simplify the result list by replacing the singleton terms (1 X)
by X._

{% highlight cl %}
CL-USER> (encode-direct '(a a a a b c c a a d e e e e))
((4 a) b (2 c) (2 a) d (4 e))
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p113.lisp)

**1.14 (\*) Duplicate the elements of a list.**

{% highlight cl %}
CL-USER> (duplicate-elems '(1 2 3))
(1 1 2 2 3 3)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p114.lisp)

**1.15 (\*\*) Duplicate the elements of a list a given number of times.**
{% highlight cl %}
CL-USER> (duplicate-elems '(1 2 3) 3)
(1 1 1 2 2 2 3 3 3)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p115.lisp)

**1.16 (\*\*) Drop every N'th element from a list.**

{% highlight cl %}
LISP-PROBLEMS> (drop '(1 2 3 4 5 6 7 8 9) 2)
(1 3 5 7 9)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p116.lisp)

**1.17 (\*) Split a list into two parts; the length of the first part is given.**

{% highlight cl %}
LISP-PROBLEMS> (split '(1 2 3 4 5) 3)
((1 2 3) (4 5))
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p117.lisp)

**1.18 (\*\*) Extract a slice from a list.**

_Given two indices, START and END, the slice is the list containing the elements between them in the original list (both limits included). Start counting the elements with 0._

{% highlight cl %}
CL-USER>  (slice '(1 2 3 4 5 6 7 9) 3 6)
(4 5 6 7)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p118.lisp)

**1.19 (\*\*) Rotate a list N places to the left.**
{% highlight cl %}
CL-USER> (rotate '(1 2 3 4 5) 2)
(3 4 5 2 1)
CL-USER> (rotate '(1 2 3 4 5) -2)
(4 5 3 2 1)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p119.lisp)

_Hint: Use the predefined functions LENGTH and APPEND, as well as the result of problem 1.17._

**1.20 (\*) Remove the n'th element from a list.**
{% highlight cl %}
CL-USER> (remove-nth '(1 2 3 4) 2)
(1 2 4)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p120.lisp)

**1.21 (\*) Insert an element at a given position into a list.**

{% highlight cl %}
CL-USER> (insert '(1 2 3 4 5) 3 10)
(3 2 1 10 4 5)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p121.lisp)

**1.22 (\*) Create a list containing all integers within a given
  range.**

{% highlight cl %}
CL-USER> (range 3 10)
(3 4 5 6 7 8 9 10)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p122.lisp)

**1.23 (\*\*) Extract a given number of randomly selected elements from a list.**

_The selected items shall be put into a result list._

{% highlight cl %}
CL-USER> (rnd-select '(1 2 3 4 5 6) 3)
(6 5 2)
CL-USER> (rnd-select '(1 2 3 4 5 6) 3)
(6 6 1)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p123.lisp)

_Hint: Use the built-in random number generator RANDOM and MY-NTH._

**1.24 (\*) Lotto: Draw N different random numbers from the set 1..M.**

_The selected numbers shall be put into a result list._

{% highlight cl %}
CL-USER> (lotto-select 6 49)
(8 15 19 5 2 13)
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p124.lisp)

_Hint: Combine the solutions of problems 1.22 and 1.23._

**1.25 (\*) Generate a random permutation of the elements of a list.**

{% highlight cl %}
CL-USER> (compress '(1 2 3))
2
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p125.lisp)

Example:
?- rnd_permu([a,b,c,d,e,f],L).
L = [b,a,d,c,e,f]

Hint: Use the solution of problem 1.23.

**1.26 (\*\*) Generate the combinations of K distinct objects chosen from the N elements of a list**
In how many ways can a committee of 3 be chosen from a group of 12 people? We all know that there are C(12,3) = 220 possibilities (C(N,K) denotes the well-known binomial coefficients). For pure mathematicians, this result may be great. But we want to really generate all the possibilities (via backtracking).

{% highlight cl %}
CL-USER> (compress '(1 2 3))
2
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p126.lisp)

Example:
?- combination(3,[a,b,c,d,e,f],L).
L = [a,b,c] ;
L = [a,b,d] ;
L = [a,b,e] ;
...

**1.27 (\*\*) Group the elements of a set into disjoint subsets.**
a) In how many ways can a group of 9 people work in 3 disjoint subgroups of 2, 3 and 4 persons? Write a predicate that generates all the possibilities via backtracking.

{% highlight cl %}
CL-USER> (compress '(1 2 3))
2
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p127.lisp)

Example:
?- group3([aldo,beat,carla,david,evi,flip,gary,hugo,ida],G1,G2,G3).
G1 = [aldo,beat], G2 = [carla,david,evi], G3 = [flip,gary,hugo,ida]
...

b) Generalize the above predicate in a way that we can specify a list of group sizes and the predicate will return a list of groups.
{% highlight cl %}
CL-USER> (compress '(1 2 3))
2
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p127.lisp)

Example:
?- group([aldo,beat,carla,david,evi,flip,gary,hugo,ida],[2,2,5],Gs).
Gs = [[aldo,beat],[carla,david],[evi,flip,gary,hugo,ida]]
...

Note that we do not want permutations of the group members; i.e. [[aldo,beat],...] is the same solution as [[beat,aldo],...]. However, we make a difference between [[aldo,beat],[carla,david],...] and [[carla,david],[aldo,beat],...].

You may find more about this combinatorial problem in a good book on discrete mathematics under the term "multinomial coefficients".

**1.28 (\*\*) Sorting a list of lists according to length of sublists**
a) We suppose that a list (InList) contains elements that are lists themselves. The objective is to sort the elements of InList according to their length. E.g. short lists first, longer lists later, or vice versa.

{% highlight cl %}
CL-USER> (compress '(1 2 3))
2
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p128.lisp)

Example:
?- lsort([[a,b,c],[d,e],[f,g,h],[d,e],[i,j,k,l],[m,n],[o]],L).
L = [[o], [d, e], [d, e], [m, n], [a, b, c], [f, g, h], [i, j, k, l]]

b) Again, we suppose that a list (InList) contains elements that are lists themselves. But this time the objective is to sort the elements of InList according to their length frequency; i.e. in the default, where sorting is done ascendingly, lists with rare lengths are placed first, others with a more frequent length come later.

{% highlight cl %}
CL-USER> (compress '(1 2 3))
2
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p128.lisp)

Example:
?- lfsort([[a,b,c],[d,e],[f,g,h],[d,e],[i,j,k,l],[m,n],[o]],L).
L = [[i, j, k, l], [o], [a, b, c], [f, g, h], [d, e], [d, e], [m, n]]

Note that in the above example, the first two lists in the result L have length 4 and 1, both lengths appear just once. The third and forth list have length 3; there are two list of this length. And finally, the last three lists have length 2. This is the most frequent length.


##Arithmetic
---

**2.01 (\*\*) Determine whether a given integer number is prime.**

{% highlight cl %}
CL-USER> (prime-p 3)
T
CL-USER> (prime-p 9)
NIL
{% endhighlight %}
[View solution](https://github.com/bbatsov/cl-99-problems/blob/master/p201.lisp)

_The Sieve of Eratosthenes is an algorithm for finding prime numbers,
that you might find helpful._

##Logic and Codes
---

##Binary Trees
---

##Multiway Trees
---

##Graphs
---

##Misc
---
