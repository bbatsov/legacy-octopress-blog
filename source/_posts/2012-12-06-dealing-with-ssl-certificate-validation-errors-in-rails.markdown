---
layout: post
title: "Dealing with SSL certificate validation errors in Rails"
date: 2012-12-06 17:07
comments: true
categories: 
- Rails
- Ruby
---

I often see this question asked - "I'm getting the following error

```
OpenSSL::SSL::SSLError: hostname was not match with the server certificate
```

when trying to deliver an email with Rails 3. How can I solve the problem?"

Obviously the best solution would be get a valid certificate for your hostname, but sometimes
this is not possible or you simply don't want to bother with this stuff (on your development machine for instance).
The solution to the problem commonly suggested is to turn off encryption completely like this:

``` ruby
ActionMailer::Base.smtp_settings = {
  :address              => 'mail.foo.com',
  :port                 => 587,
  :domain               => 'foo.com',
  :user_name            => 'addy@foo.com',
  :password             => 'foofoo',
  :authentication       => 'plain',
  :enable_starttls_auto => true
}
```

This bit of code represent a portion of your `ActionMailer` configuration and you'd put it in `application.rb` or
`env.rb` (where env is something like `development`, `staging`, `production`, etc). 

While the solution is OK for `development.rb` you'd be crazy to use
this code in production! Disabling encryption means that your username
and password will traverse the Internet in plain text! A simple, but
secure solution would be to just disable the certificate validation,
without sacrificing the secure connection:

``` ruby
ActionMailer::Base.smtp_settings = {
  :address              => 'mail.foo.com',
  :port                 => 587,
  :domain               => 'foo.com',
  :user_name            => 'addy@foo.com',
  :password             => 'foofoo',
  :authentication       => 'plain',
  :enable_starttls_auto => true,
  :openssl_verify_mode  => 'none'
}
```

This code snippet is mostly the same as the one shown before. The crucial difference is the line 
`:openssl_verify_mode => 'none'`.

I hope someone will find this short article useful. Happy hacking!
