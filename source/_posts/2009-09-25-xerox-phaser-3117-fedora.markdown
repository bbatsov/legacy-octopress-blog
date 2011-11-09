---
layout: post
title: Using Xerox Phaser 3117 on Fedora
categories:
- Hardware
- Fedora
- Linux
---

The driver selected by default by Fedora 11 is not appropriate for
Xerox Phaser 3117 - it will not print with it. However there is a very
easy solution to the problem.

Go to **System -> Administration -> Printing** (In GNOME at least, in KDE
it’s probably something similar). Right click the Xerox Phaser 3117
printer icon there and select "Properties" from the menu. Then in the
"Make and model" section choose change and then select Samsung
ML-1710.

After you apply the change you've just made, you can start printing
with your Phaser.
