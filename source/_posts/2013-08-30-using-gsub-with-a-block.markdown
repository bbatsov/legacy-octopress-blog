---
layout: post
title: "Using Ruby's gsub with a block"
date: 2013-08-30 15:29
comments: true
categories:
- Ruby
---

`String#gsub` is one of the most used Ruby methods in the wild. Just
about every Ruby programmer knows about the method and uses it fairly
regularly.

Here's a quick refresher of the typical `gsub` usage:

``` ruby
# using string match
'John Wayne'.gsub('John', 'Bruce')
=> "Bruce Wayne"

# using regexp match
'John   Wayne'.gsub(/\w+\s+(\w+)/, 'Bruce \1')
=> "Bruce Wayne"
```

Basically we can replace string and regexp matches with other
strings. When doing regexp matches we can access the matched groups
individually with `\1`, `\2`, etc and embed them in the replacement
string.  Sometimes, however, some additional processing of the matched
data might be required. Consider this trivial example - we might want
to increment a matched number by 1. Here `gsub`'s version that takes a
block comes into action:

``` ruby
# num will be passed the string '12'
'Apollo 12'.gsub(/\d+/) { |num| num.to_i.next }
=> "Apollo 13"
```

Basically we're replacing the matched portion of the string with the
result of the block. While the param enhances the readability of the code it's not necessary:

``` ruby
# we're not making use of a block param
'Apollo 12'.gsub(/(\d+)/) { Regexp.last_match[1].to_i.next }
=> "Apollo 13"
```

`Regexp.last_match[1]` is the OO version of the obscure (but pretty
popular) Perlism `$1`. In this particular case using the block param
(as in the first example) is obviously a better idea.

Note that some people expect that `gsub` would yield to the block all
the matched groups as arguments - that is not the case, you'll always
get a single argument denoting the entire regexp match.

``` ruby
# here name is 'Apollo 12' and number is blank
'Apollo 12'.gsub(/(\w+) (\d+)/) { |name, number| puts name, number }
```

Keep this in mind!

That's all for today folks! I hope you'll find this short article useful!
