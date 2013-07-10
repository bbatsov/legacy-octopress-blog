---
layout: post
title: "The Elements of Style in Ruby #7: The case against ==="
date: 2013-07-10 15:44
comments: true
categories:
- Ruby
- Style
---

Today we'll discuss the following section from the [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide):

> Avoid explicit use of the case equality operator `===`. As it name<br/>
> implies it's meant to be used implicitly by `case` expressions and<br/>
> outside of them it yields some pretty confusing code.

For those of you who don't know of the case equality operator `===` -
it's the magic behind `case` that allows us to write code like this:

``` ruby
case something
when Array then ...
when 1..100 then ...
when /some_regexp/ then ...
end
```

Ruby will convert the above code to something like:

``` ruby
case something
when Array === something then ...
when 1..100 === something then ...
when /some_regexp/ === something then...
end
```

For many classes (like `Fixnum` and `String`) `===` will behave the
same way as `==`.  On the other hand - `Module`, `Range` and `Regexp`
define customized versions of the operator method `===`.  Knowing how
these 3 classes have defined `===`, the case expression is also
equivalent to this one:

``` ruby
case something
when something.is_a? Array then ...
when 1..100.include? something then ...
when something =~ /some_regexp/ then ...
end
```

So far everything is peachy, right?

The problem with the `===` is that when some people see it they decide
it's very _cool_ and start using it all over their code instead of
its much clearer alternatives. I've seen `===` (ab)used quite often for **instance of** checks.

``` ruby
# wtf, why doesn't this work???
# extremely common mistake I've seen numerous times
return unless a === Array

# === is defined in Module
return unless Array === a # same as Array.===(a)
```

I've also seen it used many times for range inclusion
tests. Fortunately nobody has decided so far that `===` is preferable
to `=~` for regular expressions.

It should be our utmost goal as programmers to produce clear and
easily digestible code. This means we should abstain ourselves from
doing clever tricks like:

``` ruby
Array === something
(1..100) === 7
/something/ === some_string
```

And bet on clarity instead:

``` ruby
something.is_a?(Array)
(1..100).include?(7)
some_string =~ /something/
```

They don't call it the **case equality operator** for no reason - it's
meant to be used internally by `case` expressions. I guess if it were
a regular method (instead of an operator method) we'd never have had
to deal with its abuse.

As usual I'm looking forward
to hearing your thoughts here and on
[Twitter](http://twitter.com/bbatsov)!

Code long and prosper!
