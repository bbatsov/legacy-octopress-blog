---
layout: post
title: How to center a JDialog over a JFrame in Swing
categories:
- Java
- Swing
---

I always thought that the fact that JDialogs accepted a parent frame
as a constructor argument was the thing, that would make the dialog’s
position relative to that of the frame:

``` java
public JDialog(final java.awt.Frame parent, boolean modal)
```

Unfortunately all of my freshly opened dialogs would appear in the
upper left angle of my screen, not centered over the parent JFrame. I
looked around and found out that I simply needed one more method call
per dialog:

``` java
theDialog.setLocationRelativeTo(theFrame);
```

You need to call this method before the JDialog’s show() method. Now
everything is perfect and the dialog appears always right above the
center of the frame.
