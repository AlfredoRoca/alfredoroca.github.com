---
layout: post
title: "Activer record associations"
description: ""
category: [activerecord, rails] 
tags: [activerecord, associations]
---
{% include JB/setup %}

<!-- TOC START -->
<div id="dw__toc">
<h3 class="toggle">Table of Contents</h3>
<div>

<ul class="toc">
<li class="level1"><div class="li"><a href="#belongs_to_has_many">Belongs_to / has_many</a></div></li>
<li class="level1"><div class="li"><a href="#has_and_belongs_to_many">Has_and_belongs_to_many</a></div></li>
<li class="level1"><div class="li"><a href="#has_many_through_---_uniq_clause">has_many through ---  uniq clause</a></div></li>
</ul>
</div>
</div>
<!-- TOC END -->

<h1 class="sectionedit1" id="belongs_to_has_many">Belongs_to / has_many</h1>
<div class="level1">
<pre class="code"># == Schema Information
#
# Table name: emergencies
#
#  id              :integer          not null, primary key
#  activated_by_id :integer
#
# Indexes
#
#  index_emergencies_on_activated_by_id  (activated_by_id)

class Emergency &lt; ActiveRecord::Base
  belongs_to :activated_by, primary_key: &#039;id&#039;, foreign_key: &#039;activated_by_id&#039;, class_name: &#039;Company&#039;
end</pre>
<pre class="code"># == Schema Information
#
# Table name: companies
#
#  id              :integer          not null, primary key
#  name            :string

class Company &lt; ActiveRecord::Base
  has_many :emergencies, primary_key: &#039;id&#039;, foreign_key: &#039;activated_by_id&#039;, class_name: &#039;Emergency&#039;
  validates :name, presence: true, uniqueness: true
end</pre>
<pre class="code">Emergency.first.activated_by.name
Company.first.emergencies</pre>

<p>
Area has_many loops
Loop belongs_to Area
</p>
<pre class="code"># loop/index.html.erb
&lt;td&gt;&lt;%= loop.area.name %&gt;&lt;/td&gt;</pre>
<pre class="code"># area/_form.heml.erb
  &lt;div class=&quot;field&quot;&gt;
    &lt;%= f.label :area_id %&gt;&lt;br&gt;
    &lt;%= f.select :area_id, Area.all.map { |area| [area.name, area.id] }, include_blank: true %&gt;
  &lt;/div&gt;</pre>

</div>

<h1 class="sectionedit2" id="has_and_belongs_to_many">Has_and_belongs_to_many</h1>
<div class="level1">

<p>
Source: <a href="http://apidock.com/rails/ActiveRecord/Associations/ClassMethods/has_and_belongs_to_many" class="urlextern" title="http://apidock.com/rails/ActiveRecord/Associations/ClassMethods/has_and_belongs_to_many"  rel="nofollow">http://apidock.com/rails/ActiveRecord/Associations/ClassMethods/has_and_belongs_to_many</a>
</p>
<pre class="code"># == Schema Information
#
# Table name: loops
#
#  id         :integer          not null, primary key
#  name       :string
#  coord_x    :decimal(, )
#  coord_y    :decimal(, )
#  created_at :datetime
#  updated_at :datetime
#  area_id    :integer

class Loop &lt; ActiveRecord::Base
  has_and_belongs_to_many :gates
  belongs_to :area
  has_many :emergencies
  validates :name, presence: true, uniqueness: true
end</pre>
<pre class="code"># == Schema Information
#
# Table name: gates
#
#  id         :integer          not null, primary key
#  name       :string
#  coord_x    :decimal(, )
#  coord_y    :decimal(, )
#  created_at :datetime
#  updated_at :datetime
#
class Gate &lt; ActiveRecord::Base
  has_and_belongs_to_many :loops
  validates :name, presence: true, uniqueness: true
end</pre>
<pre class="code">l = Loop.first
l.gates &lt;&lt; Gate.first</pre>
<pre class="code"># loops/_add_gates.html.erb
&lt;h3&gt;Add gates&lt;/h3&gt;
&lt;%= form_tag loops_path do %&gt;
&lt;div class=&quot;field&quot;&gt;
  &lt;%= label_tag :gate %&gt;
  &lt;%= collection_select :gate, :id, Gate.all, :id, :name, include_blank: true %&gt;
&lt;/div&gt;
&lt;div class=&quot;actions&quot;&gt;
  &lt;%= submit_tag %&gt;
&lt;/div&gt;
&lt;% end %&gt;</pre>

</div>

<h1 class="sectionedit3" id="has_many_through_---_uniq_clause">has_many through ---  uniq clause</h1>
<div class="level1">
<pre class="code">class Project &lt; ActiveRecord::Base
    validates :name, presence: true, uniqueness: true
    has_many :activities
    has_many :tasks, -&gt; { uniq }, through: :activities
    has_many :users, -&gt; { uniq }, through: :activities
    scope :how_many_new_activity, -&gt; { limit(5) }
end</pre>

</div>