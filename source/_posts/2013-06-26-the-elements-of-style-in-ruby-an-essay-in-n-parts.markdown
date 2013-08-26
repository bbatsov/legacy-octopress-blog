---
layout: post
title: "The Elements of Style in Ruby: An Essay in N parts"
date: 2013-06-26 16:30
comments: true
categories:
- Ruby
---

[The Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide) is
nearing its second birthday. The project has gained more attention and
more traction than I could have imagined. For the millionth time I was
amazed by the fantastic Ruby developers around the world.

The project has also steadily evolved:

- it covers more and more aspects of programming in Ruby
- it features many more code examples
- it is now translated in several languages
- it gave birth to the automated static code analyzer [RuboCop](https://github.com/bbatsov/rubocop)
- it has become the basis for hundreds of slightly modified internal project or company style guides

One common criticism for the Ruby style guide is that it doesn't
feature extensive rationale about most of the rules in it. That's
deliberate - even now the document is pretty intimidating. If we were
to delve into the reasoning behind each and every rule, the guide's
size might come close to that of a small book.

I do, however, feel that the rationale behind some of the rules is
important. That's why I'll be starting a series of *N* posts devoted
to the topic. I'll try to cover as many of the rules as I can - from
the more straightforward ones like _maximum line length_, to the most
controversial ones like _the use of single-quoted strings when
possible_. The articles will be published in no particular order and
on no particular schedule.

Keep an eye out for the installments in the series here and on
[Twitter](http://twitter.com/bbatsov). I'm looking forward to many
interesting discussions with you!

Feel free to take a look at the
[first article in the series, dedicated to the maximum line length we should aim for](/articles/2013/06/26/the-elements-of-style-in-ruby-number-1-maximum-line-length/).

## Articles in the Series

1. [Maximum Line Length](/articles/2013/06/26/the-elements-of-style-in-ruby-number-1-maximum-line-length/)
2. [Favor sprintf(format) Over String#%](/articles/2013/06/27/the-elements-of-style-in-ruby-number-2-favor-sprintf-format-over-string-number-percent/)
3. [Make Sure Something Is an Array](/articles/2013/06/28/the-elements-of-style-in-ruby-number-3-make-sure-something-is-an-array/)
4. [Array#join vs Array#*](/articles/2013/07/01/the-elements-of-style-in-ruby-number-4-array-number-join-vs-array-number-star/)
5. [Readability of Long Numeric Literals](/articles/2013/07/02/the-elements-of-style-in-ruby-number-5-readability-of-long-numeric-literals)
6. [Attributes Redux](/articles/2013/07/04/the-elements-of-style-in-ruby-number-6-attributes-redux)
7. [The case against `===`](/articles/2013/07/10/the-elements-of-style-in-ruby-number-7-the-case-against-equals-equals-equals)
8. [Know Thy Predicates](/articles/2013/08/14/the-elements-of-style-in-ruby-number-8-know-thy-predicates/)
9. [Hash#has_key? and Hash#has_value? are deprecated](/articles/2013/08/21/the-elements-of-style-in-ruby-number-9-hash-number-has-key-and-hash-number-has-value-are-deprecated/)
