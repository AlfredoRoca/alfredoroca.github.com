---
layout: post
title: "Email configuration"
description: ""
category: [rails]
tags: [email_configuration]
---
{% include JB/setup %}

<h1 class="sectionedit1" id="email_configuration_-_shk">email configuration - SHK</h1>
<div class="level1">
<pre class="code"># /config/environment/production.rb
config.action_mailer.default_url_options = { host: &#039;www.sharingkitchn.com&#039; }</pre>
<pre class="code"># devise configuration
config.action_mailer.delivery_method = :smtp
# change to true to allow email to be sent during development
config.action_mailer.perform_deliveries = true
config.action_mailer.raise_delivery_errors = true
config.action_mailer.default :charset =&gt; &quot;utf-8&quot;
config.action_mailer.smtp_settings = {
  :port           =&gt; 587,
  :address        =&gt; &#039;smtp.gmail.com&#039;,
  :domain         =&gt; ENV[&#039;SHK_EMAIL_USERNAME&#039;],
  :authentication =&gt; :plain,
  :enable_starttls_auto =&gt; true,
  :user_name      =&gt; ENV[&#039;SHK_EMAIL_USERNAME&#039;],
  :password       =&gt; ENV[&#039;SHK_EMAIL_PASSWORD&#039;]
}</pre>

<p>
# devise.rb
</p>
<pre class="code">  config.mailer_sender = &#039;francesca+platform@sharingkitchn.com&#039;</pre>

</div>