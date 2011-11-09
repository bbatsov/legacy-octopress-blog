---
layout: post
title: "Enabling 3D support for Nouveau in Fedora 13"
categories:
- Fedora
- Linux
- Hardware
---

Most of you probably have heard that Fedora 13 will feature
experimental 3D support for the Nouveau open source driver for Nvidia
cards. This support, however, is not enabled by default. To enable it
you need to install the mesa-dri-drivers-experimental package. I,
personally, do it like this(if you haven’t configured sudo, you’ll
have to perform this as root):

``` bash
sudo yum install mesa-dri-drivers-experimental
```

Afterwards you can enable Compuz, play chromium-bsu or whatever your heart desires.
