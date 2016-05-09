---
layout: post
title: "Stop spec_helper from being loaded multiple times"
description: ""
category: [rspec, testing]
tags: []
---
{% include JB/setup %}


<https://kpumuk.info/ruby-on-rails/my-top-7-rspec-best-practices/>

Put this code at the top of spec_helper.rb

    # figure out where we are being loaded from
    if $LOADED_FEATURES.grep(/spec\/spec_helper\.rb/).any?
      begin
        raise "foo"
      rescue => e
        puts <<-MSG
      ===================================================
      It looks like spec_helper.rb has been loaded
      multiple times. Normalize the require to:

        require "spec/spec_helper"

      Things like File.join and File.expand_path will
      cause it to be loaded multiple times.

      Loaded this time from:

        #{e.backtrace.join("\n    ")}
      ===================================================
        MSG
      end
    end

