---
layout: post
title: "Default values, required arguments, keyword arguments and splats in Ruby"
description: ""
category: [ruby]
tags: [default values, arguments, splat]
---
{% include JB/setup %}

## Ruby 2 Keyword Arguments

<https://robots.thoughtbot.com/ruby-2-keyword-arguments>

    def foo(bar: 'default')
      puts bar
    end

    foo # => 'default'
    foo(bar: 'baz') # => 'baz'

    options = {bar: 'bazinga'}
    foo(options) # => 'bazinga'




## Required keyword arguments

    def foo(bar:)
      puts bar
    end

    foo # => ArgumentError: missing keyword: bar
    foo(bar: 'baz') # => 'baz'


<http://www.justinweiss.com/articles/fun-with-keyword-arguments/>

    def hello_message(greeting, time_of_day, first_name:, last_name:)
      "#{greeting} #{time_of_day}, #{first_name} #{last_name}!"
    end

    args = ["Morning"]
    keyword_args = {last_name: "Weiss"}

    hello_message("Good", *args, first_name: "Justin", **keyword_args) # => "Good Morning, Justin Weiss!"


## Splat array into a list

    def print(x,y) 
      "coordinates: (#{x},#{y})" 
    end

    print(34,45) => coordinates: (34,45)
    
    coords = [12,56]
    print(*coords) => coordinates: (12,56)

## Splat keyword argument into a argument list

    def print(x:, y:) 
      "coordinates: (#{x},#{y})" 
    end

    print(x:34, y:45) => coordinates: (34,45)
    
    coords = {x:12, y:56}
    print(**coords) => coordinates: (12,56)


## Mix of regular arguments, keyword arguments, and splats:

    def hello_message(greeting, time_of_day, first_name:, last_name:)
      "#{greeting} #{time_of_day}, #{first_name} #{last_name}!"
    end

    args = ["Morning"]
    keyword_args = {last_name: "Weiss"}

    hello_message("Good", *args, first_name: "Justin", **keyword_args) # => "Good Morning, Justin Weiss!"

## Capture arguments with * and keyword arguments with **

    def dual_argument_capturing_method(*args, **keyword_args)
      {args: args, keyword_args: keyword_args}
    end

    dual_argument_capturing_method(1, 2, 3, key: "value") # => {:args=>[1, 2, 3], :keyword_args=>{:key=>"value"}}


