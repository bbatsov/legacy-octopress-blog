---
layout: post
title: "The best way to implement the Singleton pattern in Java and
Ruby"
categories:
- Java
- Ruby
- Design Patterns
---

I haven’t posted anything lately, but I just received my brand new
**Das Keyboard** and now I simply can’t stop typing. Recently I’ve been
going through some effective technics to implement popular design
patterns and I was surprised to see how few people where aware of
them. For example since Java 5 the best way to implement the Singleton
pattern is simply to use an enum like this:

``` java
public enum SomeClass {
    INSTANCE;
}
```

This is possible due to the fact that in Java(unlike in C++ and C#)
enums are full-blown classes(although they do not support features
like inheritance for example). You get an added bonus when using an
enum class – you do not have to worry about serialization – this is
handled for you behind the scenes.

And this is how one should implement the Singleton pattern in Ruby:

``` ruby
require 'singleton'

class Some
  include Singleton
end
```

Through the magic of Ruby’s mix-ins you get a private constructor for
your class and an instance method with which you can obtain a
reference to the single instance of the class. And best of all –
because this library has undergone a substantial degree of testing it
is pretty much bulletproof. Things hardly get simpler than that.
