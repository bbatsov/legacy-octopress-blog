---
layout: post
title: "Regexp anchors in Ruby"
date: 2013-12-04 15:46
comments: true
categories:
- Ruby
---

Some Rubyists, when faced with the task of matching against the
beginning or the end of a string, are prone to using `^` and `$` in
their regular expressions. Most of the time the code will seem to work properly,
but... these anchors don't actually match a string's beginning and
end - they match a **line**'s beginning and end. Consider the
following example:

``` ruby
string = 'username'
string[/^username$/]   # matches (as expected)
string = "some injection\nusername"
string[/^username$/]   # matches again(WAT???)
```

The anchors for beginning and end of a string are actually `\A` and
`\z`(there's also a similar `\Z` anchor, but it's rarely used in
practice):

``` ruby
string = "some injection\nusername"
string[/\Ausername\z/] # don't match
```

In an actual application the line `string[/^username$/]` is a recipe for
disaster. That's why Rails 4 started raising exceptions when `^` and
`$` are used in `validates :something, format: { with: /.../ }`.

By the way, this isn't something specific to Ruby at all -  `\A` and `\z` are not the same
thing as `^` and `$` in most programming languages that have Perl-style regular expressions.

There's something peculiar in Ruby, though - it automatically uses
**multiline mode** (which enables the aforementioned behaviour of
having `^` and `$` match per line) for regular expressions. Other
languages support it as well, but usually you need to enable it
yourself, since it's not consider a particularly intuitive
default. For example - by default Perl, Java and C# treat `^` and `$` as
beginning/end of string until you **explicitly** enable **multiline match mode**
(`/m`). In Ruby `/m` simply allows `.` to match newlines.

I guess people, who've recently switched to Ruby from another
language, would be most susceptible to writing potentially dangerous
code like this.

That's all for today folks. I hope you'll find this article useful.
As usual I'm looking forward to hearing your thoughts here and on
[Twitter](http://twitter.com/bbatsov)!
