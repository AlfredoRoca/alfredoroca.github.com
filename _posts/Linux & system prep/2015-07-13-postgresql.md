---
layout: post
title: "PostgreSQL"
description: ""
category: [postgres] 
tags: [postgres]
---
{% include JB/setup %}

<!-- TOC START -->
<div id="dw__toc">
<h3 class="toggle">Table of Contents</h3>
<div>

<ul class="toc">
<li class="level1"><div class="li"><a href="#postgresql">PostgreSQL</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#attentionrails_time_zone_vs_pg_utc">Attention: Rails time zone &lt;= vs =&gt; PG UTC</a></div></li>
</ul>
</li>
<li class="level1"><div class="li"><a href="#working_with_time_zone_recommendations">Working with time zone recommendations</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#cheat_sheet">Cheat Sheet</a></div>
<ul class="toc">
<li class="level3"><div class="li"><a href="#dos">DOs</a></div></li>
<li class="level3"><div class="li"><a href="#don_ts">DON&#039;Ts</a></div></li>
</ul>
</li>
<li class="level2"><div class="li"><a href="#work_with_timezone">Work with Time.zone</a></div>
<ul class="toc">
<li class="level3"><div class="li"><a href="#good">GOOD</a></div></li>
<li class="level3"><div class="li"><a href="#cheat_sheet1">Cheat sheet</a></div></li>
</ul>
</li>
</ul>
</li>
<li class="level1"><div class="li"><a href="#testing_dates_in_timezone_with_postgres">Testing dates in timezone with postgres</a></div></li>
</ul>
</div>
</div>
<!-- TOC END -->

<h1 class="sectionedit1" id="postgresql">PostgreSQL</h1>
<div class="level1">

<p>
DO NOT configure time_zone in config/application_.rb. Instead, localize_date to user timezone.
</p>
<pre class="code"># application_helper.rb
def localize_date(date)
  I18n.l date.in_time_zone(&#039;Madrid&#039;), format: &quot;%d/%m/%Y %a, %H:%M&quot; if date
end</pre>

<p>
Convert date/time strings to timestamp with to_timestamp(..)
</p>

<p>
Query:
</p>
<pre class="code">@activities = Activity.joins(:project).select(&#039;projects.name&#039;).where(&quot;start &gt;= to_timestamp(&#039;#{params[:start]}&#039;, &#039;DD/MM/YYYY&#039;)&quot;).where(&quot;start &lt;= to_timestamp(&#039;#{params[:ended]} 23:59:59&#039;, &#039;DD/MM/YYYY HH24:MI:SS&#039;)&quot;).group(:name).sum(:duration)

@number_of_entries = Activity.where(&quot;start &gt;= to_timestamp(&#039;#{params[:start]}&#039;, &#039;DD/MM/YYYY&#039;)&quot;).where(&quot;start &lt;= to_timestamp(&#039;#{params[:ended]} 23:59:59&#039;,&#039;DD/MM/YYYY HH24:MI:SS&#039;)&quot;).count

@total_duration = Activity.where(&quot;start &gt;= to_timestamp(&#039;#{params[:start]}&#039;, &#039;DD/MM/YYYY&#039;)&quot;).where(&quot;start &lt;= to_timestamp(&#039;#{params[:ended]} 23:59:59&#039;, &#039;DD/MM/YYYY HH24:MI:SS&#039;)&quot;).sum(&#039;duration&#039;)
</pre>

</div>

<h2 class="sectionedit2" id="attentionrails_time_zone_vs_pg_utc">Attention: Rails time zone &lt;= vs =&gt; PG UTC</h2>
<div class="level2">

<p>
PostgreSQL save Ruby <strong>DateTime</strong> into <strong>timestamp</strong> UTC (WITHOUT timezone)
</p>

<p>
Function to_timestamp(date-time , format ) converts string date-time into timestamp WITH timezone, ie UTC+1  / UTC+2 summer
</p>

</div>

<h1 class="sectionedit3" id="working_with_time_zone_recommendations">Working with time zone recommendations</h1>
<div class="level1">

<p>
<a href="http://www.elabs.se/blog/36-working-with-time-zones-in-ruby-on-rails" class="urlextern" title="http://www.elabs.se/blog/36-working-with-time-zones-in-ruby-on-rails"  rel="nofollow">http://www.elabs.se/blog/36-working-with-time-zones-in-ruby-on-rails</a>
</p>

<p>
Configure: config.time_zone in config/application.rb
</p>
<ul>
<li class="level1"><div class="li"> Use: Time.zone.parse </div>
</li>
<li class="level1"><div class="li"> Use: 2.hours.ago</div>
</li>
<li class="level1"><div class="li"> Preferred Time (or DateTime) to Date because the former includes date info. Date doesn&#039;t include time info.</div>
</li>
<li class="level1"><div class="li"> Use: Date.today.in_time_zone. Never Date.today.to_time</div>
</li>
<li class="level1"><div class="li"> Quering with rails way (never SQL). Ex: Post.where([“posts.published_at &gt; ?”, Time.current])</div>
</li>
</ul>

</div>

<h2 class="sectionedit4" id="cheat_sheet">Cheat Sheet</h2>
<div class="level2">

</div>

<h3 class="sectionedit5" id="dos">DOs</h3>
<div class="level3">
<pre class="code">2.hours.ago # =&gt; Fri, 02 Mar 2012 20:04:47 JST +09:00
1.day.from_now # =&gt; Fri, 03 Mar 2012 22:04:47 JST +09:00
Date.today.in_time_zone # =&gt; Fri, 02 Mar 2012 22:04:47 JST +09:00
Date.current # =&gt; Fri, 02 Mar
Time.zone.parse(&quot;2012-03-02 16:05:37&quot;) # =&gt; Fri, 02 Mar 2012 16:05:37 JST +09:00
Time.zone.now # =&gt; Fri, 02 Mar 2012 22:04:47 JST +09:00
Time.current # Same thing but shorter. (Thank you Lukas Sarnacki pointing this out.)
Time.zone.today # If you really can&#039;t have a Time or DateTime for some reason
Time.current.utc.iso8601 # When supliyng an API (you can actually skip .zone here, but I find it better to always use it, than miss it when it&#039;s needed)
Time.strptime(time_string, &quot;%Y-%m-%dT%H:%M:%S%z&quot;).in_time_zone # If you can&#039;t use time.zone.parse</pre>

</div>

<h3 class="sectionedit6" id="don_ts">DON&#039;Ts</h3>
<div class="level3">
<pre class="code">Time.now # =&gt; Returns system time and ignores your configured time zone.
Time.parse(&quot;2012-03-02 16:05:37&quot;) # =&gt; Will assume time string given is in the system&#039;s time zone.
Time.strptime(time_string, &quot;%Y-%m-%dT%H:%M:%S%z&quot;) # Same problem as with Time#parse.
Date.today # This could be yesterday or tomorrow depending on the machine&#039;s time zone.
Date.today.to_time # =&gt; # Still not the configured time zone.</pre>

</div>

<h2 class="sectionedit7" id="work_with_timezone">Work with Time.zone</h2>
<div class="level2">

<p>
<a href="http://danilenko.org/2012/7/6/rails_timezones/" class="urlextern" title="http://danilenko.org/2012/7/6/rails_timezones/"  rel="nofollow">http://danilenko.org/2012/7/6/rails_timezones/</a>
</p>

<p>
Server in UTC+4
Client in UTC-5
</p>
<pre class="code">Time.zone = &#039;EST&#039;
DateTime.now.to_s
# =&gt; &quot;2012-07-06T13:30:00+04:00&quot;
Time.now.to_s
# =&gt; &quot;2012-07-06 13:30:00 +0400&quot;
Time.zone.now.to_s
# =&gt; &quot;2012-07-06 04:30:00 -0500&quot;</pre>
<pre class="code">Time.zone = &#039;EST&#039;
Time.now.end_of_day.to_s
# =&gt; &quot;2012-07-06 23:59:59 +0400&quot;   &gt;&gt;&lt;&lt;&lt;&lt;&gt;&gt;&lt;&lt; WRONG!!!
Time.zone.now.end_of_day.to_s
# =&gt; &quot;2012-07-06 23:59:59 -0500&quot;   &gt;&gt;&lt;&lt;&lt;&lt;&gt;&gt;&lt;&lt; GOOD!!!</pre>

</div>

<h3 class="sectionedit8" id="good">GOOD</h3>
<div class="level3">
<pre class="code">Time.zone = &#039;EST&#039;
Time.now.in_time_zone.end_of_day.to_s
# =&gt; &quot;2012-07-06 23:59:59 -0500&quot;
Time.zone.now.end_of_day.to_s
# =&gt; &quot;2012-07-06 23:59:59 -0500&quot;</pre>

</div>

<h3 class="sectionedit9" id="cheat_sheet1">Cheat sheet</h3>
<div class="level3">

<p>
Get current time
</p>
<pre class="code">Time.zone.now
Time.current</pre>

<p>
Get Day (Today, Yesterday, etc.)
</p>
<pre class="code">Time.zone.today
Time.zone.today - 1</pre>

<p>
Build time
</p>
<pre class="code">Time.zone.local(2012, 6, 10, 12, 00)</pre>

<p>
Time From Timestamp
</p>
<pre class="code">Time.zone.at(timestamp)</pre>

<p>
Parse Time (Simple)
</p>
<pre class="code">Time.zone.parse(str)</pre>

<p>
Parse time with explicit format
</p>
<pre class="code">Time.zone.parse(str, &quot;%Y-%m-%d %H:%M %Z&quot;).in_time_zone    #&lt;&lt;&lt;&lt;&lt;&lt; acceptable
Time.zone.strptime(str, &quot;%Y-%m-%d %H:%M&quot;)        # &lt;&lt;&lt;&lt; better with gem time_zone_ext [[https://github.com/doz/time_zone_ext]]</pre>

<p>
Getting time for date
</p>
<pre class="code">date.beggining_of_day</pre>

</div>

<h1 class="sectionedit10" id="testing_dates_in_timezone_with_postgres">Testing dates in timezone with postgres</h1>
<div class="level1">
<pre class="code"># factory.rb
activation_date { Time.current.utc.iso8601 }</pre>

</div>

