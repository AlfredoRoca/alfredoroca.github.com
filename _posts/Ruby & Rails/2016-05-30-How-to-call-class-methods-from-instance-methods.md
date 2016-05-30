---
layout: post
title: "How to call class methods from instance methods"
description: ""
category: [Rails, methods]
tags: []
---
{% include JB/setup %}


Using self.class.class_method

    class Foo
        def self.some_class_method
            puts self
        end

        def some_instance_method
            self.class.some_class_method
        end
    end

    print "Class method: "
    Foo.some_class_method

    print "Instance method: "
    Foo.new.some_instance_method


Outputs:

    Class method: Foo
    Instance method: Foo



