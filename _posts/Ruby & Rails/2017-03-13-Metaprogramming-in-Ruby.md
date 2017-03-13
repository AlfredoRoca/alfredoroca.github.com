---
layout: post
title: "Metaprogramming Ruby"
description: ""
category: [ruby, class_eval, instance_eval, define_method, extend]
tags: []
---
{% include JB/setup %}

# class_eval vs instance_eval

<https://www.jimmycuadra.com/posts/metaprogramming-ruby-class-eval-and-instance-eval/>

When called on a class name constant, these two methods will allow you to create methods of the opposite type from their names. MyClass.class_eval` will create instance methods and MyClass.instance_eval` will create class methods.

    class Person
    end

    Person.class_eval do
      def say_hello
       "Hello!"
      end
    end

    jimmy = Person.new
    jimmy.say_hello # "Hello!"


    class Person
    end

    Person.instance_eval do
      def human?
        true
      end
    end

    Person.human? # true


<http://web.stanford.edu/~ouster/cgi-bin/cs142-winter15/classEval.php>

class_eval is equivalent to typing the code inside a class statement

    MyClass.class_eval do
      def num
        @num
      end
    end

behaves exactly the same as the following code:

    class MyClass
      def num
        @num
      end
    end



# class_eval vs extend

Is this syntax functionally equivalent

    def self.included(base)
      base.class_eval do
        extend ClassMethods
      end
    end

to this?

    def self.included(base)
      base.extend ClassMethods
    end

Response:

The only relevant difference is that only classes respond to `class_eval`, whereas both classes and instances respond to `extend`.

If you don't plan on using your method with object instances, then they are equivalent, though the second implementation can be used to add instance methods to a particular instance, while the first one cannot.


# class_eval vs define_method

<https://tenderlovemaking.com/2013/03/03/dynamic_method_definitions.html>

Defining methods with define_method is faster, consumes less memory, and depending on your application isn’t significantly slower than using a class_eval defined method. So what is the down side?

Closures

The main down side is that `define_method` creates a closure. The closure could hold references to large objects, and those large objects will never be garbage collected. 

When using `define_method` be careful not to hold references to objects you don’t care about.
