---
layout: post
title: "RuboCop 0.14: Beyond the Ruby Style Guide"
date: 2013-10-07 14:56
comments: true
categories:
- Ruby
- RuboCop
---

Good news, everyone - [RuboCop](https://github.com/bbatsov/rubocop) 0.14 was just released!

Generally I announce RuboCop releases in only [140 characters](https://twitter.com/bbatsov),
but this time I'll make an exception. This release is more significant
than most of our recent releases for one particular reason - we've
made an effort to make more aspects of RuboCop configurable than ever
before. For instance now you can make RuboCop enforce the use of
double-quoted strings, hashes that only use hash rockets, no spaces
inside block parentheses and more of that sort.

I've started the project with the simple goal of creating a tool to help you follow the
[Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide) to the
letter - originally it didn't even have configuration options for that very reason :-)
The project, however, quickly outgrew its humble origin and became much more popular than I could have envisioned.
Today we have a core team of RuboCop hackers, dozens of contributors and thousands of users.
Having received a lot of feedback over the past year from people who use slightly
modified version of the style guide, I've come to realize that the initial
approach was hardly optimal and now supporting various popular coding
practices is one of the core values of RuboCop.

If you've abstained from trying out RuboCop, because you don't agree
with portions of the style guide - now it's a good time to take it out
for a spin. A list of all changes in 0.14 can be found
[here](https://github.com/bbatsov/rubocop/blob/master/CHANGELOG.md).
All configurable aspects of RuboCop are listed [here](https://github.com/bbatsov/rubocop/blob/master/config/default.yml).

P.S. As usual - suggestions for new features and improvements are always welcome! We can make RuboCop only as good as you want it to be!
