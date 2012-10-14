---
layout: post
title: "Ruby Tip #3: Matching on an Object's Class in a Case Expression"
date: 2012-10-14 15:23
comments: true
categories: 
- ruby
- programming
---

From time to time you might want to take different actions depending
on an object's class. One handy way to do so is with a `case`
expression:

``` ruby
case object
when Fixnum then puts 'Object is an integer number'
when String then puts 'Object is a string'
when Hash then puts 'Object is a hash'
end
```

Behind the scenes this is transformed to:

``` ruby
case object
when Fixnum === object then puts 'Object is an integer number'
when String === object then puts 'Object is a string'
when Hash === object then puts 'Object is a hash'
end
```

A lot of people seem to make the following mistake, so beware:

``` ruby
# WRONG - Class === Class will return false
case object.class
when Fixnum then puts 'Object is an integer number'
when String then puts 'Object is a string'
when Hash then puts 'Object is a hash'
end
```

Hopefully you'll find this small tip useful.

