---
layout: post
title: "Retry when rescue from error"
description: ""
category: [ruby, kernel]
tags: [rescue]
---
{% include JB/setup %}

The limited retry pattern:

    def api_call(args) 
      @retries ||= 0
      begin
        do_api_call 
      rescue ApiError, Timeout 
        @retries += 1
        retry if @retries < 5
      end
    end
