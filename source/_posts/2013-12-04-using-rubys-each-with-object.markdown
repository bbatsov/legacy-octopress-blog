---
layout: post
title: "Using Ruby's each_with_object"
date: 2013-12-04 16:29
comments: true
categories:
- Ruby
---

Sometimes we'd like to build a new collection object from the elements
of another collection.  One trivial example would be element
occurrence counting, which basically means you need to build a hash
from an array.

People coming from an imperative background will probably implement this in terms of `each` (or `for`):

``` ruby
nums = [1, 1, 2, 3, 3, 5]
result = Hash.new(0)

# with each
nums.each { |n| result[n] += 1 }

# with for
for num in nums
  result[num] += 1
end
```

This is a reasonable solution, but surely we can do better!

Rubyists fond of functional programming techniques might use `reduce` to solve the problem at hand:

``` ruby
nums = [1, 1, 2, 3, 3, 5]
nums.reduce(Hash.new(0)) { |a, e| a[e] += 1; a }
# => {1=>2, 2=>1, 3=>2, 5=>1}
```

This code works well, but it's a bit more complex than it needs to be -
mostly because of the need to return the hash explicitly in `reduce`'s block.
Enter `Enumerable#each_with_object`:

``` ruby
nums = [1, 1, 2, 3, 3, 5]
nums.each_with_object(Hash.new(0)) { |e, a| a[e] += 1 }
# => {1=>2, 2=>1, 3=>2, 5=>1}
```

`each_with_object` invokes its block for each element with an
arbitrary object argument, and returns the initially given object,
thus eliminating the need to return it ourselves as the block's
result. Simple and neat!

That's all for now, folks. I hope you'll find this article useful.
As usual I'm looking forward to hearing your thoughts here and on
[Twitter](http://twitter.com/bbatsov)!
