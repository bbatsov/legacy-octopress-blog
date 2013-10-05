---
layout: post
title: "Using Ruby's gsub with a hash"
date: 2013-10-03 16:12
comments: true
categories:
- Ruby
---

Recently we discussed [how you can use `String#gsub` with a block](http://batsov.com/articles/2013/08/30/using-gsub-with-a-block/).
Today we'll examine another somewhat unknown feature of the `gsub` method - the ability to supply a replacement hash as the second argument (which is normally a string).

If the replacement argument is a hash, and the matched text is one of its keys, the corresponding value is the replacement string. Here's a simple example:

``` ruby
def geekify(string)
  string.gsub(/[leto]/, 'l' => '1', 'e' => '3', 't' => '7', 'o' => '0')
end

geekify('leet') # => '1337'
geekify('noob') # => 'n00b'
```

Keep in mind you're not restricted to single character replacements:

``` ruby
def doctorize(string)
  string.gsub(/M(iste)?r/, 'Mister' => 'Doctor', 'Mr' => 'Dr')
end

doctorize('Mister Freeze') # => 'Doctor Freeze'
doctorize('Mr Smith')   # => 'Dr Smith'
```

That's all for today folks! I hope you'll find this short article useful!
