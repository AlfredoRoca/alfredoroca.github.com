---
layout: post
title: "HABTM association migration"
description: ""
category: [Rails]
tags: [Rails, associations, migrations, habtm]
---
{% include JB/setup %}

Where:

    class Teacher < ActiveRecord::Base
      has_and_belongs_to_many :students
    end

and

    class Student < ActiveRecord::Base
      has_and_belongs_to_many :teachers
    end

for rails 4:

    rails generate migration CreateJoinTableStudentTeacher student teacher
