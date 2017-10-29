---
layout: post
title: "PG citext type: case-insensitive text"
description: ""
category: [postgresql, rails]
tags: []
---
{% include JB/setup %}

<https://www.postgresql.org/docs/9.4/static/citext.html>

Rails migration example:

    class CreateAddress < ActiveRecord::Migration
      def change
        create_table :addresses, id: :uuid do |t|
          t.citext :name
          t.string :address

          t.timestamps null: false
          t.references :user, type: :uuid, index: true
        end
      end
    end

