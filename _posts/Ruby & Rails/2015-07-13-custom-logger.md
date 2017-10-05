---
layout: post
title: "Custom logger"
description: ""
category: [ruby, rails]
tags: [logger]
---
{% include JB/setup %}


    # lib/logger/custom_logger
    require 'singleton'

    class CustomLogger < Logger
      include Singleton
      
      def initialize
        super(Rails.root.join(&#039;log/custom_logger.log&#039;))
        self.formatter = formatter()
        self
      end

      def formatter
        Proc.new{|severity, time, progname, msg|
          formatted_severity = sprintf(&quot;%-5s&quot;,severity.to_s)
          formatted_time = time.strftime(&quot;%d-%m-%Y %H:%M:%S&quot;)
          &quot;[#{formatted_severity} #{formatted_time} #{$$}] #{msg.to_s.strip}\n&quot;
        }
      end

      class << self
        delegate :error, :debug, :fatal, :info, :warn, :add, :log, :to =&gt; :instance
      end

    end

Usage:

    CustomLogger.info("text to log")
    CustomLogger.warn("text to log")
    CustomLogger.debug("text to log")
    CustomLogger.fatal("text to log")
    CustomLogger.error("text to log")

Example

    [INFO  04-04-2015 14:12:57 18491] Processing data</pre>
