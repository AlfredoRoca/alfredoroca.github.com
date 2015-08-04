---
layout: post
title: "Javascript"
description: ""
category: [js, events, event_binding] 
tags: [js, events, event_binding]
---
{% include JB/setup %}

<h1 class="sectionedit1" id="event_binding_to_a_control_with_jquery_turbolinks">Event bindinding to a control with jQuery &amp; turbolinks</h1>
<div class="level1">
  <pre class="code">
  // evolution.js
    function hideMessage() {
    $(&#039;#message&#039;).addClass(&#039;invisible&#039;);
    };

    var ready;
    ready = function() {
      $(&#039;#emergency_evolution&#039;).on(&#039;click&#039;, function(event) {
        hideMessage();
      });
    };

    $(document).ready(ready);
    $(document).on(&#039;page:load&#039;, ready);
  </pre>

  <pre class="code">
    # evolution.html.erb
    &lt;% content_for :js do %&gt;
    &lt;%= javascript_include_tag &#039;evolution&#039;, &#039;data-turbolinks-track&#039; =&gt; true %&gt;
    &lt;script&gt;
    hideMessage();
    &lt;/script&gt;
    &lt;% end %&gt;
    ...
  </pre>
  <pre class="code"># application.html - head
    ...
    &lt;%= yield :js if content_for?(:js) %&gt;
    ...
  </pre>
  <pre class="code"># evolution.html.erb
      &lt;%= f.text_area :evolution, class: &quot;form-control&quot; %&gt;   ---&gt; id=&quot;emergency_evolution
  </pre>

</div>

<h1 class="sectionedit2" id="mini_jquery">MINI JQUERY</h1>
<div class="level1">
  <pre class="code">window.$ = function(s) {
    var c = {
    &#039;#&#039;: &#039;ById&#039;,
    &#039;.&#039;: &#039;sByClassName&#039;,
    &#039;@&#039;: &#039;sByName&#039;,
    &#039;=&#039;: &#039;sByTagName&#039;}[s[0]];
    return document[c?&#039;getElement&#039;+c:&#039;querySelectorAll&#039;](s.slice(1))
  };</pre>

  <p>
    con estos 2xx bytes y sin necesidad de jQuery, puedes hacer:
  </p>
  <pre class="code">$(&#039;#cabecera&quot;) o $(&#039;.cabecera)</pre>

</div>