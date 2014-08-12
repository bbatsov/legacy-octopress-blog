---
layout: post
title: "The State of Some Emacs Packages for Clojure Development"
date: 2014-08-12 11:29
comments: true
categories:
- Emacs
- Clojure
---

There are quite a few packages in the "official"
[clojure-emacs GitHub organization](https://github.com/clojure-emacs),
but many of them have been deprecated recently with the release of
CIDER 0.7. Unfortunately not everyone is aware of this yet and I often see
tickets related to those deprecated projects. In this short post I'll
outline the deprecations and provide a bit of background for them.

### clojure-test-mode

The venerable
[clojure-test-mode](https://github.com/clojure-emacs/clojure-mode) was
deprecated in favor of `cider-test` (which is bundled with CIDER 0.7).
`clojure-test-mode` featured quite a lot of inlined Clojure code,
which made the package very hard to maintain and reworking it to use
nREPL middleware was a no-brainer for us. `clojure-test-mode` will be
removed from the `clojure-mode` repo at some point. It also interferes
with CIDER's initialization, so you're **strongly encouraged** to get rid of it.

Down the road we might extend `cider-test` to support other test frameworks
as well (which should be feasible with different middleware providing the same interface).

### company-cider

[company-cider](https://github.com/clojure-emacs/company-cider) was deprecated, because `company-mode`
integration was added to CIDER itself (making `company-mode` the officially supported and recommended
completion library).

### ac-nrepl

[ac-nrepl](https://github.com/clojure-emacs/ac-nrepl) has been
superseded by [ac-cider](https://github.com/clojure-emacs/ac-cider).
`ac-cider` has a simpler codebase and leverages the `compliment`-based completion
introduced in CIDER 0.7. We'll probably remove `ac-nrepl` at some point in the future
to avoid the confusion between the two.


### cider-inspect

[cider-inspect](https://github.com/clojure-emacs/cider-inspect) was absorbed into CIDER 0.7.

### cider-tracing

[cider-tracing](https://github.com/clojure-emacs/cider-tracing) was superseded by middleware-based
tracing support integrated in CIDER 0.7.

## Epilogue

Those deprecations are also mentioned in the documentation of the
respective packages, but I feel it's nice to have them listed together
in a single document. Most of the packages will also emit load-time
deprecation warnings.
