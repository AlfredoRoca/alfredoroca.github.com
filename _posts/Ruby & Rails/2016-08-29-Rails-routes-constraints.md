---
layout: post
title: "Rails routes constraints"
description: ""
category: [rails, routes]
tags: [constraints]
---
{% include JB/setup %}

'routes.rb'

    resources :documents do
      collection do
        scope format: true, constaints: {format: :json} do
          get :lost
        end
      end
    end

Resultant route

    lost_documents GET    /documents/lost.:format              documents#lost {:constaints=>{:format=>:json}, :format=>/.+/}

Result:

- documents/lost.json will answer with json
- documents/lost will redirect to root route

