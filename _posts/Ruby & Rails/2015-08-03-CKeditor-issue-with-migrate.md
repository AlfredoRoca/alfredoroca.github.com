---
layout: post
title: "rake db:migrate fails with unitialized constant CKEditor"
description: ""
category: [rails, ckeditor]
tags: []
---
{% include JB/setup %}


Solution:
After gem 'rb-inotify' add gems     

    gem 'rb-fsevent'     
    gem 'rb-fchange'

And put CKEditor.rb code in comment then perform db migration. and after migration uncomment CKEditor code.

