---
layout: post
title: "Recommended Ruby books"
categories:
- Ruby
- Books
---

## Prelude

Back in the day when Ruby wasn't particularly popular outside Japan
there was only one book in English about Ruby -
["Programming Ruby"](http://www.amazon.com/Programming-Ruby-1-9-Pragmatic-Programmers/dp/1934356085/ref=sr_1_1?s=books&ie=UTF8&qid=1305641089&sr=1-1), affectionately called the Pickaxe by most
Rubyists. Those day are long gone now. Ruby on Rails propelled Ruby
into the mainstream and quite a few books on Ruby (and Rails) have
been published over the past five or so years. With so many books to
choose from developers often find it hard to pick up the _right_ book.

In this post I'll share with you my thoughts on the Ruby books that I've found
to be the most interesting and valuable. Feel free to disagree with
me, after all this is a highly subjective matter.

## Beginner books

Every saga has a beginning, every journey has a first step, every
programming language has a first book...

**[Learn to Program](http://pragprog.com/titles/ltp2/learn-to-program)**

A book that teaches programming to absolute beginners with Ruby as the
implementation language. I haven't read this book (only excerpts from
it), but I've used it as a gift for several acquaintances of mine, with the
desire to learn to program. All of them were frustrated by other
introductory books they've read and all of them praised "Learn to
Program" for its immense clarity, engaging and enjoyable style and
comprehensible examples.

**[The Well Grounded Rubyist](http://www.amazon.com/gp/product/1933988657/ref=s9_simh_gw_p14_d0_i7?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=center-2&pf_rd_r=0Q48PY008200T745JZSF&pf_rd_t=101&pf_rd_p=470938631&pf_rd_i=507846)**

"The Well Grounded Rubyist" is a thoroughly revised and updated edition
of the older book Ruby for Rails (which was 90% Ruby and 10% Rails). In this new book, author David
A. Black moves beyond Rails and presents a broader view of Ruby. It
covers Ruby 1.9 in great detail, unlike many introductory texts that
tend to offer only superficial coverage of many topics.

Starting with the basics, The Well-Grounded Rubyist explains Ruby
objects and their interactions from the ground up. In the middle
chapters, the book turns to an examination of Ruby's built-in, core
classes, showing the reader how to manipulate strings, numbers,
arrays, ranges, hashes, sets, and more. Regular expressions get
attention, as do file and other I/O operations. At 500+ pages it's a
bit of a hefty tome, but it's definitely worth reading it.

## Reference books

Reference books are not usually the biggest fun to read, but they tend
to cover everything a language has to offer and we generally keep them
close. Their value increases with the increase of our knowledge of a
particular language.

**[The Ruby Programming Language](http://www.amazon.com/Ruby-Programming-Language-David-Flanagan/dp/0596516177)**

Co-authored by Ruby's creator Matz this is without a doubt the best
analysis of the languages. Everything you need to know is explained in
a crisp and easy to comprehend manner. The thing I liked most about the
book was the depth in which all the topics were discussed - given the
superficial coverage of some topics (such as encodings) in other books,
this book really stands out. The book is full of examples and
artwork by _why the lucky stiff_, and covers both Ruby 1.8 and 1.9. The
chapters on proc & clojures and metaprogramming were particularly
strong. The books is geared mostly towards experienced programmers who
are new to Ruby. If you're one of them - it's unlikely you'll find a
better starting point in your journey to Ruby mastery.

**[Programming Ruby](http://www.amazon.com/Programming-Ruby-1-9-Pragmatic-Programmers/dp/1934356085/ref=sr_1_1?s=books&ie=UTF8&qid=1305636206&sr=1-1)**

Co-authored by the Pragmatic Programmers themselves (Dave Thomas &
Andy Hunt) this was the very first English book on Ruby (and arguably
an instrument in Ruby's international success). The first edition of
the books is freely available on-line, but it's very outdated so I
wouldn't recommend you to read it. The book has two parts
- a tutorial part and a reference part.

The tutorial part is very well written and quite readable. It's geared
towards less experienced developers and you'll not find as detailed
coverage of the topics as in "The Ruby Programming Language". You'll,
however, find full coverage of everything new in Ruby 1.9 - the book includes all the new and changed syntax and
semantics introduced since Ruby 1.8 and information about the new parameter
passing rules, local variable scoping in blocks, fibers,
multinationalization, and the new block declaration syntax.

The reference part of the book includes a description of all the
standard library modules, a complete reference for all built-in classes
and modules (including all the new and changed methods introduced by
Ruby 1.9).

I'm not sure we need the whole Ruby standard library documentation on
paper anymore in the age of the Internet, but I guess some people will
find it helpful. I just feel that the additional documentation simply
made the book heavier (and possibly pricier).

## Intermediate Ruby books

Once you've read a reference or a beginner's Ruby book you might want
to move to some book that illustrates common Ruby style, techniques
and idioms.

**[Ruby Best Practices](http://www.amazon.com/Ruby-Best-Practices-Gregory-Brown/dp/0596523009/ref=sr_1_1?ie=UTF8&qid=1305640369&sr=8-1)**

"Ruby Best Practices" is aimed at programmers who want to use Ruby as
experienced Rubyists do. Written by the developer of the Ruby project
Prawn, this concise book explains how to design beautiful APIs and
domain-specific languages with Ruby, as well as how to work with
functional programming ideas and techniques that can simplify your
code and make you more productive. You'll learn how to write code
that's readable and expressive.

The whole book is currently available from free
[on-line](http://blog.rubybestpractices.com/posts/gregory/022-rbp-now-open.html)
and has a very nice companion [blog](http://blog.rubybestpractices.com/).

**[Eloquent Ruby](http://www.amazon.com/Eloquent-Ruby-Addison-Wesley-Professional/dp/0321584104/ref=sr_1_1?s=books&ie=UTF8&qid=1305640620&sr=1-1)**

The latest (and one of the greatest) Ruby books I've read. The book
pretty much has the same aim as "Ruby Best Practices", but covers a lot
more ground and is generally a lighter and more enjoyable read. Russ
Olsen has a very particular writing style that turns even the most
boring subjects into interesting discussions. All chapters feature
some real world examples of the concepts introduced, and a discussion
of potential pitfalls.

Very highly recommended second Ruby book.

**[Design Patterns in Ruby](http://www.amazon.com/Design-Patterns-Ruby-Russ-Olsen/dp/0321490452/ref=pd_sim_b_6)**

A most enjoyable rendition of a generally boring subject by Russ Olsen. "Design
Patterns in Ruby" explores 14 of the classical GoF design patterns and
compares the canonical implementation of the patterns to idiomatic
Ruby versions of them. Every pattern features a discussion of common
use cases, pitfalls and real world usages.

The book also builds on top of the original patterns by adding a
couple of new ones like DSL and Convention over configuration.

Without a doubt one of the best Design pattern books and a must read
for all Ruby hackers. You don't need any previous knowledge of design
patterns prior to reading this book, but there are a lot of references
to the classic GoF text so you might want to read it beforehand.

## Advanced Ruby books

At some point you might want to explore some of the darker corners of Ruby.

**[Metaprogramming in Ruby](http://www.amazon.com/Metaprogramming-Ruby-Program-Like-Pros/dp/1934356476/ref=sr_1_1?s=books&ie=UTF8&qid=1305641577&sr=1-1)**

The ability to modify programs at runtime is one the greatest
strengths of Ruby, but it seems to frighten a lot of people (which is
understandable given the constant usage of fancy words like
eigenclass). If you want to sharpen your Ruby metaprogramming skills -
this is the one true book.

**[Using JRuby: Bringing Ruby to Java](http://www.amazon.com/Using-JRuby-Bringing-Ruby-Facets/dp/1934356654/ref=sr_1_1?s=books&ie=UTF8&qid=1305641415&sr=1-1)**

Believe it or not currently JRuby seems to be best Ruby implementation
around. If you're interested in using JRuby you'd do well to learn
more about the integration with the JVM that JRuby provides as well as
the various new deployment options that JRuby introduces.

This book was written by the core JRuby developers and it's absolutely
excellent. Clear and concise writing style, lots of useful examples.

## Epilogue

There are certainly other great Ruby books around that I haven't read,
but I guess that at some point reading books is just not as helpful as
writing real code. I do believe, however, that even experienced
developers can benefit from a good programming book.

So, which Ruby books that I've missed would you recommend?
