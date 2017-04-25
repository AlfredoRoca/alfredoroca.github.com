---
layout: post
title: "Belongs_to through association"
description: ""
category: [activerecord]
tags: [associations, activerecord]
---
{% include JB/setup %}

The code

    class Speech < ApplicationRecord
      belongs_to :agenda_item, -> { includes :meeting }
      delegate :meeting, to: :agenda_item
      delegate :room, to: :meeting

    class AgendaItem < ApplicationRecord
      belongs_to :meeting
      has_many :speeches, -> { order 'starting_at ASC' }, dependent: :destroy
      delegate :room, to: :meeting # this create a belongs_to room for agenda_item

    class Meeting < ApplicationRecord
      belongs_to :room
      has_many :agenda_items, -> { order 'starting_at ASC' }, dependent: :destroy
      has_many :speeches, through: :agenda_items

    class SpeechSerializer < ActiveModel::Serializer
      attributes :id, :order_num, :starting_at, :finishing_at
      belongs_to :agenda_item
      belongs_to :meeting
      belongs_to :room
    end


Association `has_many through` lets

    Meeting.last.speeches
    Room.last.meetings.map(&:speeches)

Association `delegate to` lets

    Speech.last.meeting
    Speech.last.room

