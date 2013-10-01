---
layout: post
title: "Lambdas/Procs in Case Expressions"
date: 2013-09-24 12:07
comments: true
categories:
- Ruby
---

Most Rubyists know they can use literals, classes, ranges and regular expressions in the `when` branches of a `case` expression:

``` ruby
case something
when Array then ...
when 1..100 then ...
when /some_regexp/ then ...
end
```

As you probably know `case` relies on the `===` (a.k.a. the case equality operator) being defined for
the supplied conditions. Ruby will convert the above code to something
like:

``` ruby
case something
when Array === something then ...
when 1..100 === something then ...
when /some_regexp/ === something then...
end
```

Perhaps somewhat surprisingly `===` is also defined in the `Proc` class, used to create `procs` and `lambdas`. It's defined to simply issue a `Proc#call` with the right-hand side argument of `===` as an argument:

``` ruby
is_even = ->(n) { n.even? }

is_even === 5 # => false

# same as
is_even.call(5)
```

This gives us the possibility to leverage `procs` and `lambdas` as the conditions for `when` branches. Here's a trivial example:

``` ruby
def even?
  ->(n) { n.even? }
end

def odd?
  ->(n) { n.odd? }
end

case x
when even? then puts 'even'
when odd? then puts 'odd'
else puts 'Impossible!'
end
```

You can also save a few lines by defining the lambdas inline:

``` ruby
case x
when ->(n) { n.even? } then puts 'even'
when ->(n) { n.odd? } then puts 'odd'
else puts 'Impossible!'
end
```

Things get even better if your lambdas capture some additional arguments. Consider this example checking HTTP response codes:

``` ruby
def response_code?(code)
  ->(response) { response.code == code }
end

case response
when response_code?(200) then 'OK'
when response_code?(404) then 'Not found'
else 'Unknown code'
end
```

Pretty neat, right?

That's all for today folks! Code long and prosper!
