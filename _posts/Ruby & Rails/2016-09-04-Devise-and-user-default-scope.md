---
layout: post
title: "Devise and user default scope"
description: ""
category: [rails5, devise]
tags: [default_scope]
---
{% include JB/setup %}

#Devise y default_scope en modelo User

Some Devise actions fail if default_Scope is used i User model.
For instance, the authentication fails even user and password are correct.

Create module like this

    module DeviseOverrides  
      def find_for_authentication(conditions) 
        unscoped { super(conditions) }
      end

      def serialize_from_session(key, salt)
        unscoped { super(key, salt) }
      end

      def send_reset_password_instructions(attributes={})
        unscoped { super(attributes) }
      end

      def reset_password_by_token(attributes={})
        unscoped { super(attributes) }
      end

      def find_recoverable_or_initialize_with_errors(required_attributes, attributes, error=:invalid)
        unscoped { super(required_attributes, attributes, error) }
      end

      def send_confirmation_instructions(attributes={})
        unscoped { super(attributes) }
      end

      def confirm_by_token(confirmation_token)
        unscoped { super(confirmation_token) }
      end
    end

Extend User model

    class User < ActiveRecord::Base  
      # Include default devise modules. Others available are:
      # :timeoutable and :omniauthable
      devise :database_authenticatable, :registerable,
             :recoverable, :rememberable, :trackable, :validatable,
             :confirmable, :lockable

      extend DeviseOverrides       

      default_scope -> { where(is_admin: false) }

      ...

    end

