---
layout: post
title: "Custom logger"
description: ""
category: [Logger] 
tags: [Logger]
---
{% include JB/setup %}

<h1 class="sectionedit1" id="custom_logger">Custom logger</h1>
<div class="level1">
<pre class="code"># lib/logger/custom_logger
require &#039;singleton&#039;

class CustomLogger &lt; Logger
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

  class &lt;&lt; self
    delegate :error, :debug, :fatal, :info, :warn, :add, :log, :to =&gt; :instance
  end

end
</pre>

<p>
Usage:
</p>
<pre class="code">CustomLogger.info(&quot;text to log&quot;)
CustomLogger.warn(&quot;text to log&quot;)
CustomLogger.debug(&quot;text to log&quot;)
CustomLogger.fatal(&quot;text to log&quot;)
CustomLogger.error(&quot;text to log&quot;)</pre>

<p>
Example
</p>
<pre class="code">[INFO  04-04-2015 14:12:57 18491] Processing data</pre>

</div>