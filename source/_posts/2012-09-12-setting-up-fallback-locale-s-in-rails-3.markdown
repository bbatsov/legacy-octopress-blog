---
layout: post
title: "Setting up fallback locale(s) in Rails 3"
date: 2012-09-12 14:56
comments: true
categories: 
- programming
- ruby
- rails
---

I18n(internationalization) and l10n(localization) are topics that are
covered superbly by the
[Rails Guides](http://guides.rubyonrails.org/i18n.html). The one thing
that's left out is the setup of fallback locales in case something is
missing in the currently selected locale (and mark my words -
something probably is). Therefore I'm writing this
post.

Ideally we'd have i18n-ed and localized everything perfectly, but
that's rarely the case. I'd rather have the users see things from
another locale than error messages. So how do we do that in Rails 3?
It's pretty simple actually. There are three fallback options we can
select and they all require small changes to the `application.rb` file.

* fallback to the default locale

``` ruby
# fallback to what's specified in config.i18n.default_locale
config.i18n.fallbacks = true
```

* fallback to a specified locale

``` ruby
# fallback to en, regardless of what's in config.i18n.default_locale
config.i18n.fallbacks = [:en]
```

* specify a fallback map (different fallback locales for different
  locales)
  
``` ruby  
# missing translations of es and fr languages will fallback to english
# missing translations in german will fallback to french
config.i18n.fallbacks = {'es' => 'en', 'fr' => 'en', 'de' => 'fr'}
```

Well, that's the gist of it. Happy coding!
