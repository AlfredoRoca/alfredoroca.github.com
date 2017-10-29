---
layout: post
title: "Move uniqueness validation with scope to database constraint"
description: ""
category: [rails    ]
tags: []
---
{% include JB/setup %}

Example with TODO app.


The migration to add the index 

    class AddIndexOnTitleAndUserToTodocards < ActiveRecord::Migration
      def change
        add_index :todocards, [:title, :user_id], unique: true
      end
    end

The result in the databse schema

    add_index "todocards", ["title", "user_id"], name: "index_todocards_on_title_and_user_id", unique: true


The model, doesn't need the validation on uniqueness, only needs the presence validation

    class Todocard < ActiveRecord::Base
      # now done in database level -> validates :title, presence: true, uniqueness: { scope: :user }
      validates :user_id, :title, presence: true
      belongs_to :user
    end


The controller, needs to be added the `rescue_from` clause

      def update
        begin
          respond_to do |format|
            if @todocard.update(todocard_params)
              format.html { redirect_to @todocard, notice: 'Todocard was successfully updated.' }
              format.json { render :show, status: :ok, location: @todocard }
            else
              format.html { render :edit }
              format.json { render json: @todocard.errors, status: :unprocessable_entity }
            end
          end

        rescue ActiveRecord::RecordNotUnique
          # validation at DB level
          @todocard.errors["title"] = "Title must be present and unique"
          respond_to do |format|
            format.html { render :edit }
            format.json { render json: @todocard.errors, status: :unprocessable_entity }
          end
        end
      end

      def create
        begin
          @todocard = Todocard.new(todocard_params)

          respond_to do |format|
            if @todocard.save
              format.html { redirect_to @todocard, notice: 'Todocard was successfully created.' }
              format.json { render :show, status: :created, location: @todocard }
            else
              format.html { render :new }
              format.json { render json: @todocard.errors, status: :unprocessable_entity }
            end
          end

        rescue ActiveRecord::RecordNotUnique
          # validation at DB level
          @todocard.errors["title"] = "Title must be present and unique"
          respond_to do |format|
            format.html { render :new }
            format.json { render json: @todocard.errors, status: :unprocessable_entity }
          end
        end
      end

