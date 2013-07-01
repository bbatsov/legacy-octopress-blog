---
layout: post
title: "RuboCop 0.9 is now patrolling the streets!"
date: 2013-07-01 17:06
comments: true
categories:
- Ruby
- RuboCop
---

[RuboCop](https://github.com/bbatsov/rubocop) 0.9 is finally out! This
was one of our most ambitious releases - over a month of work, ~250
commits, lots of new cops and features and a lot less bugs (OK, I'm
not sure about this, but I sincerely hope it's true). Here's the
highlights.

## Portable Linting

This is a big deal! Prior to 0.9, RuboCop piggybacked on MRI's `ruby
-wc` to find syntax errors and lint warnings. Obviously apart from
being unportable - this wasn't particularly fast (spawning processes
never is) either.

That's no longer the case - errors are now reported directly by
[Parser](https://github.com/whitequark/parser) and we've reimplemented
MRI's linting in pure Ruby into RuboCop itself. Now you'll get the
same errors and warnings on MRI, JRuby and Rubinius. And to top it
off - we've added much nicer warning messages and we report even
column information for those (MRI doesn't). This brings me to the next
point.

## Column information

All RuboCop diagnostics now feature column information as well. Now
you'll be able to jump to a problem in your code even faster. But that's not all...

## Formatter Support

We've introduced the concept of formatters (similar the to RSpec
formatter concept) and we've bundled a few formatters. We've also
changed the default output format - it now pretty similar to `clang`'s
and features extra context information:

```
spec/models/authentication_spec.rb:12:44: W: `-' interpreted as argument prefix
    }.to change(Authentication, :count).by -1
                                           ^
```

Pretty sure most of you will love this :-)

## Auto-correction Support

Running `rubocop -a` will now correct certain problems automatically. This
feature is alpha quality and just a few cops have support for it right
now. It goes without saying that you shouldn't use it on projects not under
version control (who doesn't use version control?) and without
an excellent test suite (that you undoubtedly have).

## Rails Support

`rubocop -R` will run additional Rails specific code checks. This
feature is also alpha at this point (meaning there's just one Rails
specific check at this point).

## The Road to 1.0

We plan 1.0 to be the next RuboCop major release. No new features are in
the pipeline for 1.0 - we already have so many features that require extra
work and polish anyways. If all goes well expect 1.0 by summer's end with:

* performance optimizations
* refined formatters
* enhanced auto-correction support
* lots of Rails specific checks

I hope you'll enjoy RuboCop 0.9. For the gory details, please take a
look at the epic
[Changelog](https://github.com/bbatsov/rubocop/blob/master/CHANGELOG.md).
