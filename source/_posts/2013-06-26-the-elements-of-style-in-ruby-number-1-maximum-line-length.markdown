---
layout: post
title: "The Elements of Style in Ruby #1: Maximum line length"
date: 2013-06-26 16:57
comments: true
categories:
- Ruby
---

Welcome to the first installment of **The Elements of Style in Ruby**.

We'll start off with something pretty generic, that's not specific to
Ruby at all - the maximum line length that's acceptable in our code.

The guide currently states:

> Limit lines to 80 characters.

How did we get here?

Due to limitations of the old 80-column computer screens for many
years 80 (or 79 depending on your preferences) columns has been the
gold standard for maximum line length in most languages. That was the
bulk of the reasoning behind the rule. There was also fact that Ruby's
main competitor Python upholds the same line length limit.

Many would argue that such a restriction does not make sense with the
advances in computer displays in recent years - after all a full hd
computer display would give you much more columns to play with. Why
not go with no limit what-so-ever? That would be simple, right?

Wrong! We should definitely have a limit - that's beyond any
doubt. It's common knowledge that humans read much faster vertically,
than horizontally. Try to read the source code of something with
200-character lines and you'll come to acknowledge that. On the other
hand the problem with aggressive line length limits is that they often
come at the expense of code readability - programmers start using less
descriptive variable and method names, span long expressions over
multiple lines, etc. A balance has to struck somewhere.

Ruby has generally favored succinctness (not to be confused with
terseness) and 80 columns are generally not some attainable goal as
many of you probably already know (Java developers on the other hand
can barely fit something meaningful in less that 100 or even 120
characters per line). Short, but descriptive names, proper
abstractions, judicious nesting and heredocs certainly help to keep
the lines short in Ruby.

And what of the benefit for our efforts? Apart from enabling faster
scanning though the code, shorter lines allow you to keep two or more
files opened side by side in your IDE or text editor, which is often
pretty handy. On a `1366*768` screen (somewhat unfortunately - the
most popular today) - you won't be able to achieve this with
normal-sized fonts and lines longer than 80-90 characters.

That said, maybe 80 columns is a bit too restrictive and a 100 columns
limit strikes a better balance between reading speed, code readability
and practical considerations like have two files opened side-by-side.

I'd love to hear your thoughts! Feel free to leave a comment here or
ping me on [Twitter](http://twitter.com/bbatsov).
