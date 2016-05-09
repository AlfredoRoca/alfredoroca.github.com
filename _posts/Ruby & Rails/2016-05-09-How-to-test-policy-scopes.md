---
layout: post
title: "How to test policy scopes"
description: ""
category: [pundit, testing]
tags: []
---
{% include JB/setup %}


    let(:user)         { FactoryGirl.create :user }
    let(:manager)      { FactoryGirl.create :manager }
    let(:managed_user) { FactoryGirl.create :user, manager_id: manager.id }

    before do
      sign_in manager
    end

    it "should return only his managed users" do     
      expect(UserPolicy::Scope.new(manager, User.all).resolve).to include(managed_user)
      expect(UserPolicy::Scope.new(manager, User.all).resolve).not_to include(user)
    end

