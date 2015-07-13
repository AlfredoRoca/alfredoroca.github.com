---
layout: post
title: "Rake tasks"
description: ""
category: [Rake]
tags: [Rake]
---
{% include JB/setup %}

<h1 class="sectionedit1" id="rake_tasks">Rake tasks</h1>
<div class="level1">

<p>
Example
</p>
<pre class="code">desc &quot;Setup all for app&quot;
task :setup =&gt; [&#039;db:migrate&#039;, &#039;load:categories&#039;, &#039;load:products&#039;]
namespace :load do
  desc &quot;Load categories into database&quot;
  task :categories do
    Category.delete_all
    [&#039;Electronics&#039;, &#039;Office Supplies&#039;, &#039;Toys&#039;, &#039;Clothing&#039;, &#039;Groceries&#039;].each do |name|
      Category.create!(:name =&gt; name)
    end
  end

  desc &quot;Load products into database&quot;
  task :products do
    Product.delete_all
    categories = Category.all
    words = File.readlines(&quot;/usr/share/dict/words&quot;).sort_by { rand }
    lorem = &quot;Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.&quot;
    25.times do
      Product.create!(:name =&gt; words.pop.titleize, :category =&gt; categories.rand, :description =&gt; lorem, :price =&gt; [4.99, 9.99, 14.99, 19.99, 29.99].rand)
    end
  end
end</pre>

</div>