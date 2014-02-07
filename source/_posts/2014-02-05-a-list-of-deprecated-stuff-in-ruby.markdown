---
layout: post
title: "A list of deprecated stuff in Ruby"
date: 2014-02-05 18:37
comments: true
categories:
- Ruby
---

As APIs evolve it's inevitable that portions of them will be deprecated. Generally it's fairly
easy to find out what's deprecated, but for several reasons that's not the case in Ruby:

* Deprecation is done through the use of C functions such as `rb_warn` & `rb_warning` (as opposed to some more
transparent methods as Java's `@deprecated` annotation). To see the deprecation messages from those functions
you'll have to run Ruby with `-w`. Consider this example code:

``` ruby
string.lines do |line|
  puts line
end
```

```
ruby -w test.rb

../test.rb:1: warning: passing a block to String#lines is deprecated
```

* Alternative Ruby implementations (like `JRuby` and `Rubinius`)
generally don't produce the same deprecation warnings. For instance -
`JRuby` doesn't produce any warnings for the code listed above. One
can say that currently deprecations are an MRI implementation detail
(although they shouldn't be).

* Deprecations are rarely mentioned in the API docs.

* There's no easy way to find out in which version of Ruby
something got deprecated as `rb_warn` is a generic instrumentation for
producing all sorts of warnings, as opposed to something created specifically to handle
deprecations.

* Some APIs are deprecated only informally (like
  [`Hash#has_key?` and `Hash#has_value?`](http://batsov.com/articles/2013/08/21/the-elements-of-style-in-ruby-number-9-hash-number-has-key-and-hash-number-has-value-are-deprecated/)).

* Some APIs are deprecated with `Kernel#warn` (like `Digest::Digest`).

All of the above makes it fairly hard to compile a precise list of deprecations, but we'll go
only for a rough cut here. Let see what we can do...

Grepping in Ruby 2.1's code base reveals the following:

```
dir.c
2174:    rb_warning("Dir.exists? is a deprecated name, use Dir.exist? instead");

enumerator.c
355:    rb_warn("Enumerator.new without a block is deprecated; use Object#to_enum");

ext/dbm/dbm.c
338:    rb_warn("DBM#index is deprecated; use DBM#key");

ext/gdbm/gdbm.c
453:    rb_warn("GDBM#index is deprecated; use GDBM#key");

ext/openssl/ossl_cipher.c
217:    rb_warn("arguments for %s#encrypt and %s#decrypt were deprecated; "

ext/sdbm/init.c
331:    rb_warn("SDBM#index is deprecated; use SDBM#key");

ext/stringio/stringio.c
656:    rb_warn("StringIO#bytes is deprecated; use #each_byte instead");
876:    rb_warn("StringIO#chars is deprecated; use #each_char instead");
920:    rb_warn("StringIO#codepoints is deprecated; use #each_codepoint instead");
1124:    rb_warn("StringIO#lines is deprecated; use #each_line instead");

ext/zlib/zlib.c
3892:    rb_warn("Zlib::GzipReader#bytes is deprecated; use #each_byte instead");
4174:    rb_warn("Zlib::GzipReader#lines is deprecated; use #each_line instead");

file.c
1413:    rb_warning("%sexists? is a deprecated name, use %sexist? instead", s, s);

hash.c
529:            rb_warn("ignoring wrong elements is deprecated, remove them explicitly");
934:    rb_warn("Hash#index is deprecated; use Hash#key");
3470:    rb_warn("ENV.index is deprecated; use ENV.key");

io.c
3385:    rb_warn("IO#lines is deprecated; use #each_line instead");
3436:    rb_warn("IO#bytes is deprecated; use #each_byte instead");
3590:    rb_warn("IO#chars is deprecated; use #each_char instead");
3697:    rb_warn("IO#codepoints is deprecated; use #each_codepoint instead");
11196:    rb_warn("ARGF#lines is deprecated; use #each_line instead");
11243:    rb_warn("ARGF#bytes is deprecated; use #each_byte instead");
11282:    rb_warn("ARGF#chars is deprecated; use #each_char instead");
11321:    rb_warn("ARGF#codepoints is deprecated; use #each_codepoint instead");

object.c
991:    rb_warning("untrusted? is deprecated and its behavior is same as tainted?");
1005:    rb_warning("untrust is deprecated and its behavior is same as taint");
1020:    rb_warning("trust is deprecated and its behavior is same as untaint");

proc.c
663:    rb_warn("rb_f_lambda() is deprecated; use rb_block_proc() instead");

string.c
6407:       rb_warning("passing a block to String#lines is deprecated");
6576:       rb_warning("passing a block to String#bytes is deprecated");
6665:       rb_warning("passing a block to String#chars is deprecated");
6769:       rb_warning("passing a block to String#codepoints is deprecated");

vm_method.c
54:    rb_warning("rb_clear_cache() is deprecated.");
```

Below is a cleaned up list of the output shown above. I've removed everything
that's unlikely to be of general interest.

* `Dir.exists?` is a deprecated name, use `Dir.exist?` instead
* `Enumerator.new` without a block is deprecated; use `Object#to_enum`
* `StringIO#bytes` is deprecated; use `StringIO#each_byte` instead
* `StringIO#chars` is deprecated; use `StringIO#each_char` instead
* `StringIO#codepoints` is deprecated; use `StringIO#each_codepoint` instead
* `StringIO#lines` is deprecated; use `StringIO#each_line` instead
* `File.exists?` is a deprecated name, use `File.exist?` instead
* `Hash#index` is deprecated; use `Hash#key`
* `ENV.index` is deprecated; use `ENV.key`
* `IO#lines` is deprecated; use `IO#each_line` instead
* `IO#bytes` is deprecated; use `IO#each_byte` instead
* `IO#chars` is deprecated; use `IO#each_char` instead
* `IO#codepoints` is deprecated; use `IO#each_codepoint` instead
* `ARGF#lines` is deprecated; use `ARGF#each_line` instead
* `ARGF#bytes` is deprecated; use `ARGF#each_byte` instead
* `ARGF#chars` is deprecated; use `ARGF#each_char` instead
* `ARGF#codepoints` is deprecated; use `ARGF#each_codepoint` instead
* `Object#untrusted?` is deprecated and its behavior is same as `Object#tainted?`
* `Object#untrust` is deprecated and its behavior is same as `Object#taint`
* `Object#trust` is deprecated and its behavior is same as `Object#untaint`
* passing a block to `String#lines` is deprecated
* passing a block to `String#bytes` is deprecated
* passing a block to `String#chars` is deprecated
* passing a block to `String#codepoints` is deprecated

Unfortunately there's no way to know in which version of Ruby
something got deprecated. Obviously most of the things on the list
were deprecated before Ruby 2.1. Ideally in the future we'll get a
better deprecation mechanism that actually keeps track of such data.

Hopefully some of you will find this information useful!

We're planning to get some deprecation tracking in [RuboCop](https://github.com/bbatsov/rubocop), but
due to Ruby's dynamic nature implementing such a feature reliably in a static code analyzer is an
impossible task.
