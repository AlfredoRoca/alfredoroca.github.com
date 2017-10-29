---
layout: post
title: "DB Schema with uuids"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}

Schema.db

    create_table "messages", id: :uuid, default: "uuid_generate_v4()", force: :cascade do |t|
        t.boolean  "read",       default: false
        t.uuid     "chat_id"
        t.uuid     "user_id"
        t.datetime "created_at",                 null: false
        t.datetime "updated_at",                 null: false
        t.string   "event_type"
        t.uuid     "data_id"
        t.string   "data_type"
    end

    add_index "messages", ["chat_id"], name: "index_messages_on_chat_id", using: :btree
    add_index "messages", ["data_id"], name: "index_messages_on_data_id", using: :btree
    add_index "messages", ["id"], name: "index_messages_on_id", unique: true, using: :btree
    add_index "messages", ["user_id"], name: "index_messages_on_user_id", using: :btree


Rails Migration 

    class CreateMessage < ActiveRecord::Migration
      def change
        create_table :messages, id: :uuid do |t|
          t.string :type
          t.boolean :read, default: false

          t.references :chat, type: :uuid, index: true
          t.references :user, type: :uuid, index: true

          t.timestamps null: false
        end
        add_index :messages, :id, unique: true
      end
    end
