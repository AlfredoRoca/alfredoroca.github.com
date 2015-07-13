---
layout: post
title: "Capistrano"
description: ""
category: [Capistrano, Deployment] 
tags: [Capistrano, Deployment]
---
{% include JB/setup %}

<!-- TOC START -->
<div id="dw__toc">
<h3 class="toggle">Table of Contents</h3>
<div>

<ul class="toc">
<li class="level1"><div class="li"><a href="#complete_tutorial">Complete Tutorial</a></div></li>
<li class="level1"><div class="li"><a href="#capistrano_rake_tasks">Capistrano rake tasks</a></div></li>
<li class="level1"><div class="li"><a href="#preparing_the_server">Preparing the server</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#setup_ssh">Setup SSH</a></div></li>
<li class="level2"><div class="li"><a href="#setup_deployment">Setup deployment</a></div></li>
<li class="level2"><div class="li"><a href="#manage_passwords_and_secrets">Manage passwords and secrets</a></div></li>
</ul>
</li>
<li class="level1"><div class="li"><a href="#how_to_enter_rails_console_on_production_via_capistrano">How to enter rails console on production via capistrano?</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#on_production_server">On production server</a></div></li>
<li class="level2"><div class="li"><a href="#as_a_capistrano_task">As a capistrano task</a></div></li>
</ul></li>
</ul>
</div>
</div>
<!-- TOC END -->

<h1 class="sectionedit1" id="complete_tutorial">Complete Tutorial</h1>
<div class="level1">

<p>
<a href="http://capistranorb.com/" class="urlextern" title="http://capistranorb.com/"  rel="nofollow">http://capistranorb.com/</a><br/>

<a href="http://robmclarty.com/blog/how-to-deploy-a-rails-4-app-with-git-and-capistrano" class="urlextern" title="http://robmclarty.com/blog/how-to-deploy-a-rails-4-app-with-git-and-capistrano"  rel="nofollow">http://robmclarty.com/blog/how-to-deploy-a-rails-4-app-with-git-and-capistrano</a><br/>

<a href="http://dylanmarkow.com/blog/2014/01/08/capistrano-3-setting-a-default-stage/" class="urlextern" title="http://dylanmarkow.com/blog/2014/01/08/capistrano-3-setting-a-default-stage/"  rel="nofollow">http://dylanmarkow.com/blog/2014/01/08/capistrano-3-setting-a-default-stage/</a><br/>

<a href="http://robmclarty.com/blog/how-to-deploy-a-rails-4-app-with-git-and-capistrano" class="urlextern" title="http://robmclarty.com/blog/how-to-deploy-a-rails-4-app-with-git-and-capistrano"  rel="nofollow">http://robmclarty.com/blog/how-to-deploy-a-rails-4-app-with-git-and-capistrano</a><br/>

<a href="https://github.com/bkeepers/dotenv-deployment" class="urlextern" title="https://github.com/bkeepers/dotenv-deployment"  rel="nofollow">https://github.com/bkeepers/dotenv-deployment</a><br/>

<a href="http://corlewsolutions.com/articles/article-10-how-to-deploy-rails-applications-using-capistrano-3-1-and-windows-7" class="urlextern" title="http://corlewsolutions.com/articles/article-10-how-to-deploy-rails-applications-using-capistrano-3-1-and-windows-7"  rel="nofollow">http://corlewsolutions.com/articles/article-10-how-to-deploy-rails-applications-using-capistrano-3-1-and-windows-7</a><br/>

<a href="http://vladigleba.com/blog/2014/04/10/deploying-rails-apps-part-6-writing-capistrano-tasks/" class="urlextern" title="http://vladigleba.com/blog/2014/04/10/deploying-rails-apps-part-6-writing-capistrano-tasks/"  rel="nofollow">http://vladigleba.com/blog/2014/04/10/deploying-rails-apps-part-6-writing-capistrano-tasks/</a><br/>

<a href="http://www.rubytreesoftware.com/resources/ruby-on-rails-41-ubuntu-1404-server-deployment" class="urlextern" title="http://www.rubytreesoftware.com/resources/ruby-on-rails-41-ubuntu-1404-server-deployment"  rel="nofollow">http://www.rubytreesoftware.com/resources/ruby-on-rails-41-ubuntu-1404-server-deployment</a><br/>

</p>
<pre class="code"># gemfile
# Use Capistrano for deployment
group :development do
  gem &quot;capistrano&quot;, &#039;~&gt; 3.4.0&#039;
  gem &#039;capistrano-rails&#039;, &#039;~&gt; 1.1&#039;
  gem &quot;capistrano-rvm&quot;
  # IO lib to hide password input when doing capistrano
  gem &#039;highline&#039;, &#039;~&gt; 1.7.1&#039;
  gem &#039;rvm1-capistrano3&#039;, require: false
end


$ bundle install

cd /path/to/your/project
$ bundle exec cap install
</pre>
<pre class="code"># deploy.rb
set :application, &quot;YourApplicationName&quot;
set :repo_url, &quot;git@github.com:your-username/your-repository-name.git&quot;
set :deploy_to, &quot;/path/to/your/app/in/server&quot;     -----------------&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; manually create the folder
set :deploy_via, :copy
set :rails_env, &#039;production&#039;
set :rake_env, &#039;production&#039;
set :scm, :git
set :branch, &quot;master&quot;
set :log_level, :debug
set :ssh_options, { paranoid: false }
set :pty, true
set :linked_files, fetch(:linked_files, []).push(&#039;config/database.yml&#039;, &#039;config/secrets.yml&#039;, &#039;config/deploy/production.rb&#039;)
set :linked_dirs, fetch(:linked_dirs, []).push(&#039;log&#039;, &#039;tmp/pids&#039;, &#039;tmp/cache&#039;, &#039;tmp/sockets&#039;, &#039;public/uploads&#039;)
set :keep_releases, 5
set :bundle_binstubs, -&gt; { release_path.join(&#039;bin&#039;) }</pre>
<pre class="code">#Capfile
require &#039;capistrano/setup&#039;
require &#039;capistrano/deploy&#039;
require &#039;capistrano/rvm&#039;
require &#039;capistrano/bundler&#039;
require &#039;capistrano/rails/assets&#039;
require &#039;capistrano/rails/migrations&#039;
require &#039;rvm1/capistrano3&#039;</pre>
<pre class="code"># config/deploy/production.rb
role :app, %w{deploy@example.com}
role :web, %w{deploy@example.com}
role :db,  %w{deploy@example.com}


# Extended Server Syntax
# ======================
# This can be used to drop a more detailed server definition into the
# server list. The second argument is a, or duck-types, Hash and is
# used to set extended properties on the server.

server &#039;example.com&#039;, user: &#039;user&#039;, roles: %w{web app db}, primary: true

set :deploy_to, &#039;/dir/to/app/in/production_server/&#039;
set :deploy_user, &#039;root&#039;
set :use_sudo, false
set :user, &#039;root&#039;


set :default_environment, {
  &#039;PATH&#039; =&gt; &quot;$PATH&quot;,
  &#039;RUBY_VERSION&#039; =&gt; &#039;ruby 2.2.0&#039;,
  &#039;GEM_HOME&#039;     =&gt; &#039;/home/user/.rvm/gems/ruby-2.2.0&#039;,
  &#039;GEM_PATH&#039;     =&gt; &#039;/home/user/.rvm/gems/ruby-2.2.0&#039;,
  &#039;BUNDLE_PATH&#039;  =&gt; &#039;/home/user/.rvm/gems/ruby-2.2.0&#039;  # If you are using bundler.
}</pre>

</div>

<h1 class="sectionedit2" id="capistrano_rake_tasks">Capistrano rake tasks</h1>
<div class="level1">
<pre class="code">namespace :setup do

  desc &quot;Upload deploy-production, database.yml and secrets.yml files.&quot;
  task :upload_sensitive_files do
    on roles(:app) do
      execute &quot;mkdir -p #{shared_path}/config&quot;
      upload! StringIO.new(File.read(&quot;config/database.yml&quot;)), &quot;#{shared_path}/config/database.yml&quot;
      upload! StringIO.new(File.read(&quot;config/secrets.yml&quot;)), &quot;#{shared_path}/config/secrets.yml&quot;
      execute &quot;mkdir -p #{shared_path}/config/deploy&quot;
      upload! StringIO.new(File.read(&quot;config/deploy/production.rb&quot;)), &quot;#{shared_path}/config/deploy/production.rb&quot;
    end
  end

  desc &quot;Seed the database.&quot;
  task :seed_db do
    on roles(:app) do
      within &quot;#{current_path}&quot; do
        with rails_env: :production do
          execute :rake, &quot;db:seed&quot;
        end
      end
    end
  end

  desc &quot;Symlinks config files for Nginx and Unicorn.&quot;
  task :symlink_config do
    on roles(:app) do
      execute &quot;rm -f /etc/nginx/sites-enabled/default&quot;

      execute &quot;ln -nfs #{current_path}/config/nginx.conf /etc/nginx/sites-enabled/#{fetch(:application)}&quot;
      # execute &quot;ln -nfs #{current_path}/config/unicorn_init.sh /etc/init.d/unicorn_#{fetch(:application)}&quot;
   end
  end

end</pre>

</div>

<h1 class="sectionedit3" id="preparing_the_server">Preparing the server</h1>
<div class="level1">
<pre class="code">sudo groupadd deploy
sudo useradd deploy
sudo passwd deploy
visudo  --&gt; añadir linea deploy ALL=(ALL) ALL
sudo usermod -G deploy deploy
sudo chown -R deploy:deploy deploy_to_path
sudo chmod g+w deploy_to_path</pre>

<p>
Enable passwordless sudo for user deploy
</p>
<pre class="code">visudo (como root, y añadir)
deploy ALL=NOPASSWD:/etc/init.d/nginx</pre>

</div>

<h2 class="sectionedit4" id="setup_ssh">Setup SSH</h2>
<div class="level2">

<p>
<a href="http://robmclarty.com/blog/how-to-setup-a-production-server-for-rails-4" class="urlextern" title="http://robmclarty.com/blog/how-to-setup-a-production-server-for-rails-4"  rel="nofollow">http://robmclarty.com/blog/how-to-setup-a-production-server-for-rails-4</a><br/>

</p>
<pre class="code">cp /etc/ssh/sshd_config ~
vi /etc/ssh/sshd_config

# sshd_config
Port 22222
PermitRootLogin no
...
AllowUsers deploy alfredo    ---&gt; at the very bottom of the file</pre>

<p>
Restart the service
</p>
<pre class="code">service ssh restart
/etc/init.d/ssh restart
systemctl restart sshd</pre>

</div>

<h2 class="sectionedit5" id="setup_deployment">Setup deployment</h2>
<div class="level2">
<pre class="code">$ cap production rvm:check</pre>
<pre class="code">$ cap production deploy
$ cap production setup:upload_sensitive_files
$ cap production deploy

Login server, cd /app_folder/releases/&lt;release&gt; and execute
$ bundle exec rake db:create
$ bundle exec rake db:seed</pre>

</div>

<h2 class="sectionedit6" id="manage_passwords_and_secrets">Manage passwords and secrets</h2>
<div class="level2">

<p>
Create .env_vars with
</p>
<pre class="code">SHARINGKITCHN_SECRET_KEY_BASE=5e29f57f14c304f21d0ebc6a83c1634dae9c3c2ecf49c1eb7398edd12905b4341428a8bf6103aa3cdd4d832e1a99677d8529e1627248a108a8f153a3947f8769
SHARINGKITCHN_DATABASE_PASSWORD=&lt;pw&gt;</pre>

<p>
En deploy.rb
</p>
<pre class="code">set :linked_files, %w{config/database.yml config/.env-vars}</pre>

<p>
Add to .gitignore
database.yml
.env_vars
</p>

<p>
Copy manually to shared folder/config
</p>

</div>

<h1 class="sectionedit7" id="how_to_enter_rails_console_on_production_via_capistrano">How to enter rails console on production via capistrano?</h1>
<div class="level1">

</div>

<h2 class="sectionedit8" id="on_production_server">On production server</h2>
<div class="level2">
<pre class="code">bundle exec rails console</pre>

</div>

<h2 class="sectionedit9" id="as_a_capistrano_task">As a capistrano task</h2>
<div class="level2">
<pre class="code">namespace :rails do
  desc &quot;Remote console&quot;
  task :console, :roles =&gt; :app do
    run_interactively &quot;bundle exec rails console #{rails_env}&quot;
  end

  desc &quot;Remote dbconsole&quot;
  task :dbconsole, :roles =&gt; :app do
    run_interactively &quot;bundle exec rails dbconsole #{rails_env}&quot;
  end
end

def run_interactively(command)
  server ||= find_servers_for_task(current_task).first
  exec %Q(ssh #{user}@#{myproductionhost} -t &#039;#{command}&#039;)
end</pre>
<pre class="code">cap rails:console</pre>

</div>