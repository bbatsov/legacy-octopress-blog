---
layout: post
title: "Deleting Remote Git Branches"
date: 2012-12-16 10:10
comments: true
categories: 
- git
---

This post is mostly a note to myself, since I constantly forget how to
delete remote Git branches.

The classic way to do so (introduced in Git 1.5) would be:

``` bash
$ git push origin :branch-to-delete
```

So, if I were migrating an application from MySQL to PostgreSQL I might want to delete
the `postgres` branch when I'm done:

``` bash
$ git push origin :postgres
```

You have to agree this syntax is hardly something one can easily
remember(and I'm extra certain nobody would have guessed it on their
own). Fortunately in Git 1.7 a nicer alternative to the above command
was introduced:

``` bash
$ git push origin --delete branch-to-delete
```

That's all from me for today. Now go ahead and delete those unneeded Git branches.

P.S. GitHub users might also want to take a look at this
[article](https://github.com/blog/1335-tidying-up-after-pull-requests)
describing recently added functionality to clean up after pull
requests.
