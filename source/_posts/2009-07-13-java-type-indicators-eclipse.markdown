---
layout: post
title: Java type indicators in Eclipse
categories:
- Java
- Eclipse
---

One of the things that I don’t like about the default Eclipse settings
for Java development is that in the package explorer all Java files
appear in the same manner(with the same icon). There is no visual
distinction between abstract and concrete classes, enums, interfaces...
Luckily for us Eclipse supports such a distinction and all you have to
do is enable it.

Go to **Window -> Preferences -> General -> Appearance -> Label
Decorations** and mark the check box saying **Java Type
Indicator**. I've tested this on Eclipse 3.5 only, but I guess it is
included in previous releases as well.

Eclipse, though not as feature rich as IntelliJ IDEA, offers a lot of features that one has to find for himself.
