---
layout: post
title: "Sublime Text 3"
description: ""
category: 
tags: []
---
{% include JB/setup %}

<!-- TOC START -->
<div id="dw__toc">
<h3 class="toggle">Table of Contents</h3>
<div>

<ul class="toc">
<li class="level1"><div class="li"><a href="#package_manager">Package manager</a></div></li>
<li class="level1"><div class="li"><a href="#plugins">Plugins</a></div></li>
<li class="level1"><div class="li"><a href="#user_preferences">User preferences</a></div></li>
<li class="level1"><div class="li"><a href="#key_bindings_user">Key bindings User</a></div></li>
</ul>
</div>
</div>
<!-- TOC END -->

<h1 class="sectionedit1" id="package_manager">Package manager</h1>
<div class="level1">

<p>
<a href="https://packagecontrol.io/installation#st3" class="urlextern" title="https://packagecontrol.io/installation#st3"  rel="nofollow">https://packagecontrol.io/installation#st3</a>
</p>

</div>

<h1 class="sectionedit2" id="plugins">Plugins</h1>
<div class="level1">

<p>
Alignment<br/>

BracketHighlighter<br/>

Colorpicker<br/>

Emmet<br/>

DocBlockr<br/>

Better Coffee​Script<br/>

Sublime Linter + plugins for Ruby, <abbr title="Cascading Style Sheets">CSS</abbr> <br/>

</p>

</div>

<h1 class="sectionedit3" id="user_preferences">User preferences</h1>
<div class="level1">
<pre class="code">{
  &quot;auto_complete_triggers&quot;:
  [
    {
      &quot;characters&quot;: &quot;ng-controller=\&quot;*&quot;,
      &quot;selector&quot;: &quot;punctuation.definition.string&quot;
    }
  ],
  &quot;color_scheme&quot;: &quot;Packages/Color Scheme - Default/Monokai.tmTheme&quot;,
  &quot;ignored_packages&quot;:
  [
    &quot;Vintage&quot;
  ],
  &quot;rulers&quot;:
  [
    80
  ],
  &quot;save_on_focus_lost&quot;: true,
  &quot;tab_size&quot;: 2,
  &quot;translate_tab_to_spaces&quot;: true
  &quot;translate_tabs_to_spaces&quot;: true,
}
</pre>

</div>

<h1 class="sectionedit4" id="key_bindings_user">Key bindings User</h1>
<div class="level1">
<pre class="code">[
  { &quot;keys&quot;: [&quot;ctrl+7&quot;], &quot;command&quot;: &quot;toggle_comment&quot;, &quot;args&quot;: { &quot;block&quot;: false } },
  { &quot;keys&quot;: [&quot;ctrl+shift+7&quot;], &quot;command&quot;: &quot;toggle_comment&quot;, &quot;args&quot;: { &quot;block&quot;: true } },
  { &quot;keys&quot;: [&quot;super+shift+r&quot;],  &quot;command&quot;: &quot;reindent&quot; }
]</pre>

</div>