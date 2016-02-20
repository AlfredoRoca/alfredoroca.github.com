---
layout: post
title: "How to pass messages from model to controller"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}


my_controller.rb

    def procedure_invocation
      result = @my_model.my_method
      if result[:success].present?
        redirect_to some_path
      else # error
        @message = result[:error]
        render 'some_page_with_message_error'
      end
    end

my_model.rb

    def my_method
      if everything_is_ok
        return { success: "true" }
      else
        return { error: "Something went wrong" }
      end
    end

Returning data and message

In model:

    return [data, { success: "true" }]
    return [nil, { error: "Something went wrong" }]

In controller

    @data, @message = @my_model.my_method




