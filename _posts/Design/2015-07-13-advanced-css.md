---
layout: post
title: "Advanced CSS"
description: ""
category: [CSS, design] 
tags: [CSS, design, flexbox]
---
{% include JB/setup %}

<!-- TOC START -->
<div id="dw__toc">
<h3 class="toggle">Table of Contents</h3>
<div>

<ul class="toc">
<li class="level1"><div class="li"><a href="#flexbox">Flexbox</a></div></li>
<li class="level1"><div class="li"><a href="#flex_box_items_-_flex-basis">Flex box items - flex-basis</a></div></li>
<li class="level1"><div class="li"><a href="#footer_at_least_at_the_bottom_of_the_page">footer at least at the bottom of the page:</a></div></li>
<li class="level1"><div class="li"><a href="#truncate_long_texts_with_css_text-overflow">truncate long texts with CSS &quot;text-overflow&quot;</a></div></li>
</ul>
</div>
</div>
<!-- TOC END -->

<h1 class="sectionedit1" id="flexbox">Flexbox</h1>
<div class="level1">

<p>
Flexbox
</p>

<p>
Assuming this layout:
</p>
<pre class="code">&lt;div class=&quot;row&quot;&gt;
  &lt;div class=&quot;col&quot;&gt;...&lt;/div&gt;
  &lt;div class=&quot;col&quot;&gt;...&lt;/div&gt;
&lt;/div&gt;</pre>

<p>
With flexbox, same height is just one declaration:
</p>
<pre class="code">.row {
  display: flex; /* equal height of the children */
}

.col {
  flex: 1; /* additionally, equal width */
}</pre>

<p>
Browser support: <a href="http://caniuse.com/flexbox;" class="urlextern" title="http://caniuse.com/flexbox;"  rel="nofollow">http://caniuse.com/flexbox;</a> demo: <a href="http://jsfiddle.net/sdsgW/" class="urlextern" title="http://jsfiddle.net/sdsgW/"  rel="nofollow">http://jsfiddle.net/sdsgW/</a>
</p>

</div>

<h1 class="sectionedit2" id="flex_box_items_-_flex-basis">Flex box items - flex-basis</h1>
<div class="level1">
<pre class="code">@media (min-width: 992px) {
  .flex-item-info {  flex: 1 0 auto;                  /* NEW, Spec - Opera 12.1, Firefox 20+ Chrome 42+ */
@media (max-width: 991px) {
  .flex-item-info { flex: 1 0 0;                  /* NEW, Spec - Opera 12.1, Firefox 20+ Chrome 42+ */</pre>

</div>

<h1 class="sectionedit3" id="footer_at_least_at_the_bottom_of_the_page">footer at least at the bottom of the page:</h1>
<div class="level1">

<p>
css:
</p>
<pre class="code">.footer-wrapper {
  position: relative;
  min-height: 100%;
}</pre>
<pre class="code">.footer {
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
}</pre>

<p>
html:
</p>
<pre class="code">body
  .footer-wrapper
    .footer</pre>

<p>
<a href="http://stackoverflow.com/questions/306252/how-to-align-checkboxes-and-their-labels-consistently-cross-browsers" class="urlextern" title="http://stackoverflow.com/questions/306252/how-to-align-checkboxes-and-their-labels-consistently-cross-browsers"  rel="nofollow">http://stackoverflow.com/questions/306252/how-to-align-checkboxes-and-their-labels-consistently-cross-browsers</a>
</p>

</div>

<h1 class="sectionedit4" id="truncate_long_texts_with_css_text-overflow">truncate long texts with CSS &quot;text-overflow&quot;</h1>
<div class="level1">

<p>
<abbr title="HyperText Markup Language">HTML</abbr>
</p>
<pre class="code">&lt;div id=&quot;greetings&quot;&gt;
  Hello universe!
&lt;/div&gt;</pre>

<p>
<abbr title="Cascading Style Sheets">CSS</abbr>
</p>
<pre class="code">#greetings { 
  width: 100px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis; // This is where the magic happens
}</pre>

</div>