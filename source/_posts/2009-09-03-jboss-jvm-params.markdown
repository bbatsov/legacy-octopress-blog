---
layout: post
title: Mofidy JVM parameters for JBoss AS
categories:
- Java
- JBoss
---

Most people have been in a situation requiring them to change one or
more of the parameters passed to the JVM on top of which JBoss AS is
running. For instance - you may need a bigger heap, bigger perm gen
size or something else. The best place to put these parameters is
probably the following file:

**$JBOSS_HOME/bin/run.conf**

where **$JBOSS_HOME** refers to the directory in which you’ve unpacked the JBoss AS distribution.

Look for this section:

``` bash
if [ "x$JAVA_OPTS" = "x" ]; then
    JAVA_OPTS="..."
fi
```

All you have to do now is adapt it to your needs.
