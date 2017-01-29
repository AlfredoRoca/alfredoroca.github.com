---
layout: post
title: "Change model validation error message"
description: ""
category: [rails, activerecord, I18n]
tags: [translations]
---
{% include JB/setup %}

<http://guides.rubyonrails.org/i18n.html#translations-for-active-record-models>

# app/models/user.rb
    # ...
    validates_format_of :password, :with => PASSWORD_FORMAT,
    # ...

# config/locales/en.yml
    en:
      activerecord:
        errors:
          models:
            user:
              attributes:
                password:
                  invalid: 'Must include uppercase & number'

- for ```validates_presence_of``` keyword you can use ```blank```
- for ```validates_length_of``` keyword you can use ```too_short``` or ```too_long```
- for ```validates_uniqueness_of``` keyword you can use ```taken``` 


