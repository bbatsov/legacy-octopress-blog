---
layout: post
title: "The Elements of Style in Ruby #10: In cryptic Perlisms we do not trust"
date: 2013-09-05 11:41
comments: true
categories:
- Ruby
- Style
---

For better or for worse Perl had significant influence over Ruby's
initial design. A lot of things were directly borrowed from Perl, but
over the years the Ruby community rejected most of the Perlisms. In
this article I'll go over most of the Perl legacy which you should try
to steer clear from.

### Global variables

Global variables are the nemesis of object-oriented programming(most
OO languages don't even have the concept of a global variable). Don't
introduce any of those in your Ruby programs! In most cases you can
substitute them for module instance variables:

``` ruby
# bad
$foo_bar = 1

#good
module Foo
  class << self
    attr_accessor :bar
  end
end

Foo.bar = 1
```

Unfortunately, one cannot code Ruby and get away without using the built-in global
variables...

### Special global variables

Originally Ruby borrowed just about all of Perl's special global
variables, known worldwide for their **intention revealing names** -
`$:`, `$;`, `$!`, `$$`, `$\`, etc. I've coded Ruby for quite some time now and
still can't remember what half of those meant (and I knew a bit of
Perl before I knew any Ruby). Luckily at some point the
[English library](http://www.ruby-doc.org/stdlib-2.0/libdoc/English/rdoc/English.html)
was added to Ruby, which simply adds sensible aliases for the cryptic
Perl names. With it you can change this code:

``` ruby
$:.unshift File.dirname(__FILE__)

files = `git ls-files`.split($\)
```

to:

``` ruby
require 'English'
$LOAD_PATH.unshift File.dirname(__FILE__)

files = `git ls-files`.split($INPUT_RECORD_SEPARATOR)
```

I think that the improvement is pretty obvious.  Why `English` is not required by
default is beyond me. Personally I use it always and I think you should do the same.


### Last regexp captures

When you do a regexp match (like `/regexp/ ~= string`) a few special
global variables with funky names get populated with the prematch,
match, postmatch, etc. If the regexp has any groups in it, the stuff
they matched gets assigned to other special variables with the
descriptive names `$1` (for the first group), `$2` (for the second
group), etc. This idiom is unfortunately very popular with Ruby
developers, likely because few of them know of `Regexp.last_match`.

``` ruby
/(regexp)/ =~ string
...

# this is Perl-style
process $1

# this is the same, but more clear and more object oriented
process Regexp.last_match[1]
```

Basically you can extract from `Regexp.last_match` everything you'd get from the special global variables.

Yep, you'll have to type more, but when clarity is at stake a little bit of extra typing is certainly justified.

You can even go a step further and use the `Regexp#match` method:

``` ruby
md = /(Bat.+)\s/.match('Batman rules!')
#=> #<MatchData "Batman " 1:"Batman">
md[1]
#=> "Batman"
```

By the way, keep in mind that it's generally a good idea to use named
regexp groups over positional ones, once you're dealing with more than
two groups. Numbers simply don't convey that much meaning...

### BEGIN/END blocks

Strictly speaking those came from `awk`, but I still consider them
part of the Perl legacy. If you don't know what I'm talking about feel
free to skip this section - your soul has already been saved.

``` ruby
END {
  puts "Exiting..."
}

puts "Processing..."

BEGIN {
  puts "Starting..."
}
```

`BEGIN` blocks are executed before everything else in your program in
the order in which they are encountered. `END` blocks are executed right before
the program exits. Those hideous constructs mess with the flow of
control of the program and are totally useless. I've never ever needed
a `BEGIN` block and `END` blocks are totally replaceable with
`Kernel#at_exit`. I guess they might have some utility for old-school
scripting tasks, but application developers should ignore them
completely!

### Flip-flops

Same as in the previous section - if you don't know what I'm talking about feel free to
skip this section - your soul has already been saved.

Flip-flops are an obscure conditional construct with just a single useful application - text processing:

``` ruby
DATA.each_line do |line|
  print line if (line =~ /begin/)..(line =~ /end/)
end

__END__
0a
1begin
2c
3end
4e
5f
6begin
7end
8i
9j
```

This will print:

```
1begin
2c
3end
6begin
7end
```

Hopefully you've managed to deduce how they work from this example, if
you haven't - you've just understood what their main problem is.

I never had to use those and probably you won't have a reason to use them
either. Their usage is likely going to do just one thing for you - reduce the
readability of the code you're writing.

### Epilogue

I'd really love to see some of those Perlisms out of Ruby - the
removal of `flip-flops` and `BEGIN/END` gets suggested upstream every
now and then and might happen in Ruby 3.0. Removing the global
variables, however, is unlikely to ever happen since that would be a
huge change.

You can use [RuboCop](https://github.com/bbatsov/rubocop)
to identify and fix such shortfalls of your code.

As usual I'm looking forward to hearing your thoughts here and on
[Twitter](http://twitter.com/bbatsov)!
