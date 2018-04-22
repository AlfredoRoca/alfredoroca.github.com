---
layout: post
title: "Ruby send vs __send__"
description: ""
category: [ruby]
tags: []
---
{% include JB/setup %}

In Ruby module Forwardable, you can find the following line

```
#{accessor}.__send__(:#{method}, *args, &block)
```

This lets delegate some method to another class simplifying the code. For example,

Instead of writing

```
class Owner
    def phone
        '457364'
    end
end
class Space
    def phone
        owner.phone
    end
    def owner
        @owner ||= Owner.new
    end
end
```

is shorter and easier to read

```
require 'forwardable'
class Owner
    def phone
        '457364'
    end
end
class Space
    extend Forwardable
    delegate :phone => :owner

    def owner
        @owner ||= Owner.new
    end
end
```

I want to explain why it uses ```__send__``` instead of ```send```.

The ```send``` method can be override. Example:

```
class Foo
    def __send__(*args, &block)
        false
    end
    def bar
        true
    end
end

Foo.new.bar
=> true
Foo.new.send(:bar)
=> false
Foo.new.__send__(:bar)
=> true
```

To avoid conflicts, specially in gems or libraries when the context where it will be used is unknown, always use ```__send__```.

Ruby warns when trying to redefine it:

```
warning: redefining `__send__' may cause serious problems
```
