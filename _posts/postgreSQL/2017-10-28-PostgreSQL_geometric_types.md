---
layout: post
title: "PostgreSQL geometric types"
description: ""
category: [postgresql, rails]
tags: []
---
{% include JB/setup %}

<https://www.postgresql.org/docs/9.5/static/datatype-geometric.html>

DB Schema

      create_table "positions", id: :uuid, default: "uuid_generate_v4()", force: :cascade do |t|
        t.point    "coords",      null: false
        t.datetime "created_at",  null: false
        t.datetime "updated_at",  null: false
        t.uuid     "provider_id"
        t.uuid     "address_id"
      end

      add_index "positions", ["address_id"], name: "index_positions_on_address_id", using: :btree
      add_index "positions", ["id"], name: "index_positions_on_id", unique: true, using: :btree
      add_index "positions", ["provider_id"], name: "index_positions_on_provider_id", using: :btree

Rails migration

    class CreatePosition < ActiveRecord::Migration
      def change
        create_table :positions, id: :uuid do |t|
          t.point :coords, null: false
          t.timestamps null: false

          t.references :provider, type: :uuid, index: true
          t.references :address, type: :uuid, index: true
        end
        add_index :positions, :id, unique: true
      end
    end

