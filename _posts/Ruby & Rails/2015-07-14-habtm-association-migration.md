---
layout: post
title: "HABTM association migration"
description: ""
category: [rails]
tags: [associations, migrations, habtm]
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

Or

    rails g migration CreateEmergencyExternalResourceJoinTable emergency:references external_resources:references

Gives

    class CreateJoinTableEmergencyExternalResource < ActiveRecord::Migration
      def change
        create_join_table :emergencies, :external_resources do |t|
          # t.index [:emergency_id, :external_resource_id]
          # t.index [:external_resource_id, :emergency_id]
        end
      end
    end

Wanted index must be uncommented before migrating.

In this case, index name generated is too long. Must be shortened specifying its name

    class CreateJoinTableEmergencyExternalResource < ActiveRecord::Migration
      def change
        create_join_table :emergencies, :external_resources do |t|
          t.index [:emergency_id, :external_resource_id], name: 'idx_emergency_external_resource'
          # t.index [:external_resource_id, :emergency_id]
        end
      end
    end
