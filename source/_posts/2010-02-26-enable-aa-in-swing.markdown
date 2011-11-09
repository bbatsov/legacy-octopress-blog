---
layout: post
title: "How to enable font anti-aliasing in a Java Swing app"
categories:
- Java
- Swing
---

If you have access to the source, you can do this in the main method:

``` java
// enable anti-aliasing
System.setProperty("awt.useSystemAAFontSettings","on");
System.setProperty("swing.aatext", "true");
```

Alternatively (and if you do not have access to the source, or if you find this
easier) you can simply pass the system properties above to the JVM by
adding these options to the command line:

``` java
-Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
```
