---
layout: post
title: "The % notation in ruby"
description: ""
category: [ruby]
tags: []
---
{% include JB/setup %}

# %Q, %q, %W, %w, %x, %r, %s, %i

Perl-inspired notation to quote strings: by using % (percent character) and specifying a delimiting character.

Any single non-alpha-numeric character can be used as the delimiter, ```%[including these]```, ```%?or these?```, ```%~or even these things~```.

## Strings

### % or %Q

Use %Q only for strings that contain both single quotes and double quotes, or for dynamic strings that contain double quotes.

_interpolated string_

This is an alternative for double-quoted strings, when you have more quote characters in a string.Instead of putting backslashes in front of them, you can easily write:

    >> %Q(Joe said: "Frank said: "#{what_frank_said}"")
    => "Joe said: "Frank said: "Hello!"""

The parenthesis “(…)” can be replaced with any other non-alphanumeric characters and non-printing characters (pairs), so the following commands are equivalent:

    >> %Q!Joe said: "Frank said: "#{what_frank_said}""!
    >> %Q[Joe said: "Frank said: "#{what_frank_said}""]
    >> %Q+Joe said: "Frank said: "#{what_frank_said}""+

You can use also:

    >> %/Joe said: "Frank said: "#{what_frank_said}""/
    => "Joe said: "Frank said: "Hello!"""

### %q

_non-interpolated string_

Used for single-quoted strings.The syntax is similar to %Q, but single-quoted strings are not subject to expression substitution or escape sequences.

    >> %q(Joe said: 'Frank said: '#{what_frank_said} ' ')
    => "Joe said: 'Frank said: '\#{what_frank_said} ' '"

## Arrays
 
### %W

_interpolated array of words, separated by whitespace_

Used for double-quoted array elements.The syntax is similar to %Q

    >> %W(#{foo} Bar Bar\ with\ space)
    => ["Foo", "Bar", "Bar with space"]
 
### %w

_non-interpolated array of words, separated by whitespace_

Used for single-quoted array elements. The syntax is similar to %Q, but single-quoted elements are not subject to expression substitution or escape sequences.

    >> %w(#{foo} Bar Bar\ with\ space)
    => ["\#{foo}", "Bar", "Bar with space"]

### %I

_interpolated array of symbols, separated by whitespace_

Generates an array of symbols, similar to %W, available in ruby >= 2.1.

    >> %I(#{foo} Bar Bar\ with\ space)
    => => [:foo, :Bar, :"Bar with space"]


### %i

_non-interpolated array of symbols, separated by whitespace_

Generates an array of symbols, similar to %W, available in ruby >= 2.1.

    >> %I(#{foo} Bar Bar\ with\ space)
    => [:"\#{foo}", :Bar, :"Bar with space"]

## Symbols

### %s

_interpolated string_

Used for symbols. It’s not subject to expression substitution or escape sequences.

    >> %s(foo)
    => :foo

    >> %s(foo bar)
    => :"foo bar"

    >> %s(#{foo} bar)
    => :"\#{foo} bar"

## Shell command

### %x

_interpolated shell command_

Uses the ` method and returns the standard output of running the command in a subshell.The syntax is similar to %Q.

    >> %x(echo foo:#{foo})
    => "foo:Foo\n"

## Regexp

### %r

_interpolated regexp_

Used for regular expressions.The syntax is similar to %Q.

    >> %r(/home/#{foo})
    => "/\\/home\\/Foo/"

Additionnaly, you can add flags after the closing delimiter, like this

    >> %r/[a-z]/i
    => /[a-z]/i
