---
layout: post
title: "Sorcery & RSpec"
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
<li class="level1"><div class="li"><a href="#test_model_with_sorcery_authentication">Test model with Sorcery authentication</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#to_pass_the_tests_in_views_use">To pass the tests, in views use</a></div></li>
<li class="level2"><div class="li"><a href="#user_specrb">user_spec.rb</a></div></li>
<li class="level2"><div class="li"><a href="#factorygirl">FactoryGirl</a></div></li>
<li class="level2"><div class="li"><a href="#spec_support_sorceryrb">spec/support/sorcery.rb</a></div></li>
<li class="level2"><div class="li"><a href="#spec_helperrb">spec_helper.rb</a></div></li>
<li class="level2"><div class="li"><a href="#speed_up_tests_changing_encryption_algorithm_to_md5">Speed up tests changing encryption algorithm to md5</a></div></li>
</ul>
</li>
<li class="level1"><div class="li"><a href="#testing_forms_with_multiple_parameters">Testing forms with multiple parameters</a></div></li>
</ul>
</div>
</div>
<!-- TOC END -->

<h1 class="sectionedit1" id="test_model_with_sorcery_authentication">Test model with Sorcery authentication</h1>
<div class="level1">

<p>
See ActivityLogger application<br/>

</p>

</div>

<h2 class="sectionedit2" id="to_pass_the_tests_in_views_use">To pass the tests, in views use</h2>
<div class="level2">

<p>
Evaluate &#039;current_user&#039; to avoid “undefined method `admin?&#039; for nil:NilClass”
</p>
<pre class="code">if current_user &amp;&amp; current_user.admin?</pre>

</div>

<h2 class="sectionedit3" id="user_specrb">user_spec.rb</h2>
<div class="level2">
<pre class="code">require &#039;rails_helper&#039;

describe &quot;Integration test&quot;, type: :feature do
  
  before(:each) do
    admin = FactoryGirl.create(:user_admin)
    login_user_post(admin.email, &quot;123&quot;)
  end

  it &quot;signs me in&quot; do
    expect(page).to have_content &#039;You are being redirected&#039;
  end

  context &quot;when checking validations&quot; do
    it &quot;rejects without name&quot; do
      user = FactoryGirl.build :user, name: &quot;&quot;
      expect(user.valid?).to be false
      expect(user.errors[&quot;name&quot;].present?).to be true
    end

...</pre>

</div>

<h2 class="sectionedit4" id="factorygirl">FactoryGirl</h2>
<div class="level2">
<pre class="code">FactoryGirl.define do
  factory :user do
    factory :user_admin do
      name                  {Faker::Name.name}
      email                 {Faker::Internet.email}
      admin                 {true}
      password              {&quot;123&quot;}
      password_confirmation {&quot;123&quot;}
    end
  end
end
</pre>

</div>

<h2 class="sectionedit5" id="spec_support_sorceryrb">spec/support/sorcery.rb</h2>
<div class="level2">
<pre class="code">module Sorcery
  module TestHelpers
    module Rails
      module Integration
        def login_user_post(email, password)
          page.driver.post(user_sessions_url, { email: email, password: password } )
        end
      end
    end
  end
end </pre>

</div>

<h2 class="sectionedit6" id="spec_helperrb">spec_helper.rb</h2>
<div class="level2">
<pre class="code">  config.include Sorcery::TestHelpers::Rails::Controller, type: :controller
  config.include Sorcery::TestHelpers::Rails::Integration, type: :feature</pre>

</div>

<h2 class="sectionedit7" id="speed_up_tests_changing_encryption_algorithm_to_md5">Speed up tests changing encryption algorithm to md5</h2>
<div class="level2">
<pre class="code">Rails.application.config.sorcery.configure do |config|
  config.user_config do |user|
    user.encryption_algorithm = :md5 if Rails.env.test?
  end
end</pre>

</div>

<h1 class="sectionedit8" id="testing_forms_with_multiple_parameters">Testing forms with multiple parameters</h1>
<div class="level1">

<p>
Application: SAAP
</p>
<pre class="code"># gates_controller_spec.rb
describe &quot;POST add loop&quot; do
    it &quot;adds a loop to the gate&quot; do
      gate = Gate.create! valid_attributes
      loop = FactoryGirl.create :loop
      expect { 
        post :add_loop, {id: gate.id, :loop =&gt; {:id =&gt; loop.id}}
        }.to change(gate.loops, :count).by(1)
    end
  end</pre>
<pre class="code"># _add_loops.html.erb
&lt;h3&gt;Add loops&lt;/h3&gt;
&lt;%= form_tag :area_add_loop do %&gt;
  &lt;div class=&quot;field&quot;&gt;
    &lt;%= label_tag :loop %&gt;
    &lt;%= collection_select nil, nil, Loop.all, nil, nil, include_blank: true %&gt;
  &lt;/div&gt;
  &lt;div class=&quot;actions&quot;&gt;
    &lt;%= submit_tag :Add %&gt;
  &lt;/div&gt;
&lt;% end %&gt;</pre>
<pre class="code">class GatesController &lt; ApplicationController
  before_action :set_gate, only: [:show, :edit, :update, :destroy, :add_loop, :remove_loop]

  def add_loop
    unless (loop_id = params[&#039;loop&#039;][&#039;id&#039;]).empty?
      loop = Loop.find(loop_id)
      @gate.loops &lt;&lt; loop unless @gate.loops.include?(loop)
    end
    render :edit
  end
...  </pre>

</div>
