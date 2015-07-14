---
layout: post
title: "HABTM association migration"
description: ""
category: [Rails]
tags: [Rails, associations, migrations, habtm]
---
{% include JB/setup %}

Where:

    class Emergency < ActiveRecord::Base
      has_many :external_resources
    end

and

    class ExternalResource < ActiveRecord::Base
      has_and_belongs_to_many :emergencies
    end


for rails 4:

    rails g migration CreateJoinTableEmergencyExternalResource emergency external_resource

Gives

    class CreateJoinTableEmergencyExternalResource < ActiveRecord::Migration
      def change
        create_join_table :emergencies, :external_resources do |t|
          # t.index [:emergency_id, :external_resource_id]
          # t.index [:external_resource_id, :emergency_id]
        end
      end
    end

Wanted index must be uncommented before migrating
