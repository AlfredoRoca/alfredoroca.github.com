---
layout: post
title: "Belongs_to through association"
description: ""
category: [activerecord]
tags: [associations, activerecord]
---
{% include JB/setup %}

    class Speech < ApplicationRecord
      belongs_to :agenda_item, -> { includes :meeting }
      delegate :meeting, to: :agenda_item

    class AgendaItem < ApplicationRecord
      belongs_to :meeting
      has_many :speeches, -> { order 'starting_at ASC' }, dependent: :destroy

    class Meeting < ApplicationRecord
      has_many :agenda_items, -> { order 'starting_at ASC' }, dependent: :destroy
      has_many :speeches, through: :agenda_items

Association `has_many through` lets

    Meeting.last.speeches

Association `delegate to` lets

    Speech.last.meeting

