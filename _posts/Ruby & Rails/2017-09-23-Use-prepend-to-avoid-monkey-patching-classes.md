---
layout: post
title: "Prepend module to avoid monkey patching classes"
description: ""
category: [ruby, oop]
tags: []
---
{% include JB/setup %}

Source: <https://www.justinweiss.com/articles/rails-5-module-number-prepend-and-the-end-of-alias-method-chain/>

Imagine this class

    class Point
      def to_s
        puts "Point (X1,Y1)"    
      end  
    end

    Point.new.to_s
    #=> Point (X1,Y1)

Imagine a child class that inherits from parent class Point

    class SpecialPoint < Point
      def to_s
        puts "Special "
        super
      end
    end 

    puts SpecialPoint.new.to_s
    #=> Special
    #=> Point (X1,Y1)

Point & SpecialPoint are not accessible, like in a gem.

Imagine you want to customize the `to_s` ooutput.
You can do the following.

    module Extra
      def to_s
        puts "Extra must be the first comment "
        super
      end
    end


Including the module is not working as desired

    SpecialPoint.send(:include, Extra)
    puts SpecialPoint.new.to_s
    => Special
    => Extra must be the first comment
    => Point (X1,Y1)

`Prepend` comes to the rescue!

    SpecialPoint.send(:prepend, Extra)
    puts SpecialPoint.new.to_s
    => Extra must be the first comment
    => Special
    => Point (X1,Y1)

