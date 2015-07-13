---
layout: post
title: "Spring & Guard"
description: ""
category: [Spring, Guard]
tags: [Spring, Guard, Test]
---
{% include JB/setup %}

<h1 class="sectionedit1" id="spring_guard">Spring &amp; Guard</h1>
<div class="level1">

<p>
Spring to speed up tests<br/>

Guard to automate them – starts specific tests when detects file changes<br/>

Source: <a href="http://girders.org/blog/2014/02/06/setup-rails-41-spring-rspec-and-guard/" class="urlextern" title="http://girders.org/blog/2014/02/06/setup-rails-41-spring-rspec-and-guard/"  rel="nofollow">http://girders.org/blog/2014/02/06/setup-rails-41-spring-rspec-and-guard/</a><br/>

Extract: 
</p>
<pre class="code">group :development, :test do
  gem &#039;spring-commands-rspec&#039;
  gem &#039;guard-rspec&#039;
end</pre>
<pre class="code">spring binstub --all
* bin/rake: spring already present
* bin/rspec: generated with spring
* bin/rails: spring already present</pre>
<pre class="code">spring status </pre>
<pre class="code">spring stop </pre>

<p>
To generate the guardfile:
</p>
<pre class="code">guard init</pre>

<p>
Edit the line:
</p>
<pre class="code">guard :rspec, cmd:&quot;spring rspec&quot; do</pre>

<p>
Run:
</p>
<pre class="code">guard
11:48:02 - INFO - Guard is using TerminalTitle to send notifications.
11:48:02 - INFO - Guard::RSpec is running
11:48:02 - INFO - Guard is now watching at &#039;/home/alfredo/projects/activity_logger&#039;
[1] guard(main)&gt;</pre>

<p>
If you need to change something basic in your app, such as adding a gem, updating a local dependency that could be cached, you need to restart both guard and spring
</p>

<p>
<strong>»»&gt; Restart guard »»»&gt; Ctrl-D at the console where guard is running</strong>
</p>

</div>
<div class='secedit editbutton_section editbutton_1'><form class="button btn_secedit" method="post" action="/wikimemo/doku.php"><div class="no"><input type="hidden" name="do" value="edit" /><input type="hidden" name="rev" value="1423088527" /><input type="hidden" name="summary" value="[Spring &amp; Guard] " /><input type="hidden" name="target" value="section" /><input type="hidden" name="range" value="1-1122" /><input type="hidden" name="id" value="spring_guard" /><input type="submit" value="Edit" class="button" title="Spring &amp; Guard" /></div></form></div>
<h1 class="sectionedit2" id="guardfile">Guardfile</h1>
<div class="level1">

<p>
LiverReload gem:   gem &#039;guard-livereload&#039;
Execute $ guard init livereload to add it to guardfile
Notice the part for watching factories to eecute test on controllers, models and views.
ActiveSupport/inflector is needed for &#039;singularize&#039; function
</p>
<pre class="code"># guarfile
require &#039;active_support/inflector&#039;

# A sample Guardfile
# More info at https://github.com/guard/guard#readme

## Uncomment and set this to only include directories you want to watch
# directories %w(app lib config test spec feature)

## Uncomment to clear the screen before every task
# clearing :on

## Guard internally checks for changes in the Guardfile and exits.
## If you want Guard to automatically start up again, run guard in a
## shell loop, e.g.:
##
##  $ while bundle exec guard; do echo &quot;Restarting Guard...&quot;; done
##
## Note: if you are using the `directories` clause above and you are not
## watching the project directory (&#039;.&#039;), the you will want to move the Guardfile
## to a watched dir and symlink it back, e.g.
#
#  $ mkdir config
#  $ mv Guardfile config/
#  $ ln -s config/Guardfile .
#
# and, you&#039;ll have to watch &quot;config/Guardfile&quot; instead of &quot;Guardfile&quot;

# Note: The cmd option is now required due to the increasing number of ways
#       rspec may be run, below are examples of the most common uses.
#  * bundler: &#039;bundle exec rspec&#039;
#  * bundler binstubs: &#039;bin/rspec&#039;
#  * spring: &#039;bin/rspec&#039; (This will use spring if running and you have
#                          installed the spring binstubs per the docs)
#  * zeus: &#039;zeus rspec&#039; (requires the server to be started separately)
#  * &#039;just&#039; rspec: &#039;rspec&#039;


guard &#039;livereload&#039; do
  watch(%r{app/views/.+\.(erb|haml|slim)$})
  watch(%r{app/helpers/.+\.rb})
  watch(%r{public/.+\.(css|js|html)})
  watch(%r{config/locales/.+\.yml})
  # Rails Assets Pipeline
  watch(%r{(app|vendor)(/assets/\w+/(.+\.(css|js|html|png|jpg))).*}) { |m| &quot;/assets/#{m[3]}&quot; }
end

guard :rspec, cmd: &quot;spring rspec&quot; do
  require &quot;guard/rspec/dsl&quot;
  dsl = Guard::RSpec::Dsl.new(self)
  
  # Feel free to open issues for suggestions and improvements

  # RSpec files
  rspec = dsl.rspec
  watch(rspec.spec_helper) { rspec.spec_dir }
  watch(rspec.spec_support) { rspec.spec_dir }
  watch(rspec.spec_files)

  # Ruby files
  ruby = dsl.ruby
  dsl.watch_spec_files_for(ruby.lib_files)

  # Rails files
  rails = dsl.rails(view_extensions: %w(erb haml slim))
  dsl.watch_spec_files_for(rails.app_files)
  dsl.watch_spec_files_for(rails.views)

  watch(rails.controllers) do |m|
    [
      rspec.spec.(&quot;routing/#{m[1]}_routing&quot;),
      rspec.spec.(&quot;controllers/#{m[1]}_controller&quot;),
      rspec.spec.(&quot;acceptance/#{m[1]}&quot;)
    ]
  end

  # Rails config changes
  watch(rails.spec_helper)     { rspec.spec_dir }
  watch(rails.routes)          { &quot;#{rspec.spec_dir}/routing&quot; }
  watch(rails.app_controller)  { &quot;#{rspec.spec_dir}/controllers&quot; }

  # Capybara features specs
  watch(rails.view_dirs)     { |m| rspec.spec.(&quot;features/#{m[1]}&quot;) }

  # Turnip features and steps
  watch(%r{^spec/acceptance/(.+)\.feature$})
  watch(%r{^spec/acceptance/steps/(.+)_steps\.rb$}) do |m|
    Dir[File.join(&quot;**/#{m[1]}.feature&quot;)][0] || &quot;spec/acceptance&quot;
  end

  # Factories
  watch(%r{spec/factories/(.+).rb$}) do |m|
    &quot;spec/controllers/#{m[1]}_controller_spec.rb&quot;
    &quot;spec/models/#{m[1].singularize}_spec.rb&quot;
    &quot;spec/views/#{m[1]}&quot;
  end

end</pre>

</div>