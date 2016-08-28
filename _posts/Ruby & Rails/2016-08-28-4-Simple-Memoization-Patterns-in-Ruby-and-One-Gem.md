---
layout: post
title: "4 Simple Memoization Patterns in Ruby (and One Gem)"
description: ""
category: [ruby]
tags: [memoization]
---
{% include JB/setup %}


<http://www.justinweiss.com/articles/4-simple-memoization-patterns-in-ruby-and-one-gem/>

# Super basic memoization

    class User < ActiveRecord::Base
      def twitter_followers
        # assuming twitter_user.followers makes a network call
        @twitter_followers ||= twitter_user.followers
      end
    end


## Multi-line memoization

    class User < ActiveRecord::Base
      def main_address
        @main_address ||= begin
          maybe_main_address = home_address if prefers_home_address?
          maybe_main_address = work_address unless maybe_main_address
          maybe_main_address = addresses.first unless maybe_main_address
        end
      end
    end



Gem Memoist: <https://github.com/matthewrudy/memoist>
