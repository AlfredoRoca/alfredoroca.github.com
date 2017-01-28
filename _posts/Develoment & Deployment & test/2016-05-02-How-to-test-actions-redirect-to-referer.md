---
layout: post
title: "How to test actions that redirect to request.referer"
description: ""
category: [rspec, test]
tags: []
---
{% include JB/setup %}

Solution: set request referer

    describe "POST #add_user" do
      it "adds a new user to the selected plan" do
        @request.env['HTTP_REFERER'] = root_url  # <<<<--------!
        plan = FactoryGirl.create :plan
        expect {
          post :add_user, {:id => plan.to_param, :user => {:id => keeper.to_param}}, valid_session
        }.to change(plan.users, :count).by(1)
      end
    end


