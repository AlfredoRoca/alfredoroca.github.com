---
layout: post
title: "Ejemplo JBuilder"
description: ""
category: [rails,jbuilder,ruby]
tags: []
---
{% include JB/setup %}

    class Person
      attr :name, :age
      # ... Class Definition ... #
      def initialize(name, age)
          @name = name
          @age = age
      end
     
      def to_builder
        Jbuilder.new do |person|
          person.(self, :name, :age)
        end
      end
    end

    class Company
      attr :name
      # ... Class Definition ... #
      def initialize(name, person)
          @name = name
          @person = person
      end
     
      def to_builder
        Jbuilder.new do |company|
          company.(self, :name)
          company.president person.to_builder
        end
      end
    end

    company = Company.new('Doodle Corp', Person.new('John Stobs', 58))
    company.to_builder.target!

    => "{\"name\":\"Doodle Corp\",\"president\":{\"name\":\"John Stobs\",\"age\":58}}"

