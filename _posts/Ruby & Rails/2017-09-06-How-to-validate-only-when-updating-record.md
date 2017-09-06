---
layout: post
title: "How to validate only when updating record"
description: ""
category: [rails, activerecord]
tags: [validation contexts]
---
{% include JB/setup %}

Source: 

<http://www.justinweiss.com/articles/a-lightweight-way-to-handle-different-validation-situations/>

<https://gist.github.com/dhh/9672827>

<http://api.rubyonrails.org/classes/ActiveModel/Validations.html#method-i-valid-3F>

<http://blog.arkency.com/2014/04/mastering-rails-validations-contexts/>

Validation option `on: :update` doesn't work as expected. Solution: user validation context.

Example:

    class User < ActiveRecord::Base
      validates :nick, presence: true, on: :update
      ...
    end

In rails console:

    User.create(email:"paco@paco.com", password: "123123123", password_confirmation:"123123123")

    User.last.valid?
    => false
    **Shouldn't it be valid?**

    User.last.valid?(:update)
    => false

    User.last.errors.messages
    => {}
    **then, shouldn't it appear 'nick'?**

    User.last.update(nick:"nick")
    User.last.valid?
    => true

Solution: 

**Use validation contexts**

    class User < ActiveRecord::Base
      validates :nick, presence: true, on: :updating_record
      ...
    end

In rails console:

    User.create(email:"pepe@pepe.com", password: "123123123", password_confirmation:"123123123")

    User.last.valid?
    => true

    User.last.valid?(:updating_record)
    => false

    User.last.update(nick: "nick")
    User.last.valid?(:updating_record)
    => true
