---
layout: post
title: "devise_token_auth with an existing Rails application"
description: ""
category: [rails, security]
tags: []
---
{% include JB/setup %}

Following <https://github.com/lynndylanhurley/devise_token_auth>

After `rails g devise_token_auth:install User auth` I had to change generated migration by

    class DeviseTokenAuthUpdateUsers < ActiveRecord::Migration[5.1]
      def change
        add_column :users, :tokens, :json
      end
    end

The User model, I left unchanged devise modules

      devise :database_authenticatable, :recoverable, :rememberable, :trackable, :validatable


and routes by

      namespace :api do
        scope :v1 do
          mount_devise_token_auth_for 'User', at: 'auth'
        end
      end

because exiting routes