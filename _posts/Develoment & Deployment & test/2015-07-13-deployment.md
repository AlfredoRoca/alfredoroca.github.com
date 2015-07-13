---
layout: post
title: "Deployment"
description: ""
category: [Deployment] 
tags: [Deployment]
---
{% include JB/setup %}

<!-- TOC START -->
<div id="dw__toc">
<h3 class="toggle">Table of Contents</h3>
<div>

<ul class="toc">
<li class="level1"><div class="li"><a href="#deployment_to_nairobi">Deployment to Nairobi</a></div></li>
<li class="level1"><div class="li"><a href="#deploymentshk">Deployment: ShK</a></div></li>
<li class="level1"><div class="li"><a href="#reinicio_instancias_thin_-_shk">Reinicio instancias thin - SHK</a></div></li>
<li class="level1"><div class="li"><a href="#saapfirst_deploy_in_nairobi">SAAP: First deploy in nairobi</a></div></li>
<li class="level1"><div class="li"><a href="#saapnext_deployments">SAAP: next deployments</a></div></li>
<li class="level1"><div class="li"><a href="#rollback">Rollback</a></div></li>
<li class="level1"><div class="li"><a href="#rails_console">Rails console</a></div></li>
<li class="level1"><div class="li"><a href="#tutorials">Tutorials</a></div></li>
<li class="level1"><div class="li"><a href="#code">Code</a></div></li>
<li class="level1"><div class="li"><a href="#matar_proceso_server">Matar proceso server</a></div></li>
<li class="level1"><div class="li"><a href="#create_new_postgres_user_with_password">Create new postgres user with password</a></div></li>
<li class="level1"><div class="li"><a href="#production_vars">Production vars</a></div></li>
<li class="level1"><div class="li"><a href="#bash_file_to_start_rails_server">bash file to start rails server</a></div></li>
<li class="level1"><div class="li"><a href="#nginx_thin">nginx &amp; Thin</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#install_thin">Install thin</a></div></li>
<li class="level2"><div class="li"><a href="#thin_commands_by_instances_applications">Thin commands by instances (applications)</a></div></li>
<li class="level2"><div class="li"><a href="#nginx_config">nginx config</a></div></li>
<li class="level2"><div class="li"><a href="#nginx_restart">nginx restart</a></div></li>
<li class="level2"><div class="li"><a href="#nginx_start_stop">nginx start/stop</a></div></li>
<li class="level2"><div class="li"><a href="#nginx_reload_if_changes_nginxconf">nginx reload if changes nginx.conf</a></div></li>
</ul>
</li>
<li class="level1"><div class="li"><a href="#testing_with_saap_project">Testing with SAAP project</a></div></li>
<li class="level1"><div class="li"><a href="#deploying_rails_app_using_nginx_puma_and_capistrano_3">Deploying Rails app using Nginx, Puma and Capistrano 3</a></div></li>
<li class="level1"><div class="li"><a href="#setting_up_nginx_with_rails">Setting up Nginx with Rails</a></div></li>
<li class="level1"><div class="li"><a href="#staging_server">STAGING server</a></div></li>
<li class="level1"><div class="li"><a href="#views_in_beta">views in beta</a></div></li>
</ul>
</div>
</div>
<!-- TOC END -->

<p>
<a href="http://www.rubytreesoftware.com/resources/ruby-on-rails-41-ubuntu-1404-server-deployment" class="urlextern" title="http://www.rubytreesoftware.com/resources/ruby-on-rails-41-ubuntu-1404-server-deployment"  rel="nofollow">http://www.rubytreesoftware.com/resources/ruby-on-rails-41-ubuntu-1404-server-deployment</a><br/>

<a href="http://www.gotealeaf.com/blog/deploy-rails-apps-with-capistrano" class="urlextern" title="http://www.gotealeaf.com/blog/deploy-rails-apps-with-capistrano"  rel="nofollow">http://www.gotealeaf.com/blog/deploy-rails-apps-with-capistrano</a><br/>

<a href="http://blog.mohitkanwal.com/blog/2013/04/10/deploying-rails-on-nginx-and-thin/" class="urlextern" title="http://blog.mohitkanwal.com/blog/2013/04/10/deploying-rails-on-nginx-and-thin/"  rel="nofollow">http://blog.mohitkanwal.com/blog/2013/04/10/deploying-rails-on-nginx-and-thin/</a><br/>

</p>

<h1 class="sectionedit1" id="deployment_to_nairobi">Deployment to Nairobi</h1>
<div class="level1">

<p>
Fedora + nginx
</p>
<ol>
<li class="level1"><div class="li"> production.rb ⇒ </div>
<ol>
<li class="level2"><div class="li"> config.assets.compile = true, </div>
</li>
<li class="level2"><div class="li"> config.serve_static_files = ENV[&#039;RAILS_SERVE_STATIC_FILES&#039;].present? || true</div>
</li>
</ol>
</li>
<li class="level1"><div class="li"> Create new postrges user with password as configures in database.yml</div>
</li>
<li class="level1"><div class="li"> ftp (sin tmp ni log)</div>
</li>
<li class="level1"><div class="li"> cambio a root (si el usuario no es sudoer)</div>
</li>
<li class="level1"><div class="li"> cd &lt;appdir&gt; ⇒ crea gemset</div>
</li>
<li class="level1"><div class="li"> regreso a usuario</div>
</li>
<li class="level1"><div class="li"> bundle install –without development test (pide password (sudoer))</div>
</li>
<li class="level1"><div class="li"> env vars - see below</div>
</li>
<li class="level1"><div class="li"> rake db:create</div>
</li>
<li class="level1"><div class="li"> rake db:migrate</div>
</li>
<li class="level1"><div class="li"> rake db:seed</div>
</li>
</ol>

<p>
Extract from <a href="https://github.com/rails/spring" class="urlextern" title="https://github.com/rails/spring"  rel="nofollow">https://github.com/rails/spring</a><br/>

</p>

<p>
Deployment
</p>

<p>
You must not install Spring on your production environment. To prevent it from being installed, provide the –without development test argument to the bundle install command which is used to install gems on your production machines:
</p>
<pre class="code">$ bundle install --without development test</pre>

<p>
Spring removal
</p>
<ol>
<li class="level1"><div class="li"> &#039;Unspring&#039; your bin/ executables: <code>bin/spring binstub –remove –all</code></div>
</li>
<li class="level1"><div class="li"> Remove spring from your Gemfile</div>
</li>
</ol>

</div>

<h1 class="sectionedit2" id="deploymentshk">Deployment: ShK</h1>
<div class="level1">

<p>
TO ALSER:
</p>
<pre class="code">cap staging deploy</pre>

<p>
TO NAIROBI
</p>
<pre class="code">cap production deploy</pre>
<pre class="code">ssh nairobi.pres.in  --&gt; enter password
su  --&gt; enter root password
/etc/init.d/thin restart   OR  thin restart -C /etc/thin/shk.yml</pre>

<p>
Check if rails server can start
</p>
<pre class="code">curl 0.0.0.0:3010</pre>

</div>

<h1 class="sectionedit3" id="reinicio_instancias_thin_-_shk">Reinicio instancias thin - SHK</h1>
<div class="level1">

<p>
Con el fichero para de configuración para permitir manejar las instancias de thin por separado:
</p>
<pre class="code">thin restart -C /etc/thin/shk.yml</pre>

</div>

<h1 class="sectionedit4" id="saapfirst_deploy_in_nairobi">SAAP: First deploy in nairobi</h1>
<div class="level1">
<pre class="code">cap production deploy:check_write_permissions</pre>
<pre class="code">cap production deploy</pre>

<p>
Fails because database still doesn&#039;t exist.
</p>

<p>
Prepare database.yml and secrets.yml in development pc
</p>
<pre class="code">cap production setup:upload_yml</pre>

<p>
In the production server, create the database in the release folder
</p>
<pre class="code">rake db:create</pre>

<p>
Configure thin configuration file
</p>
<pre class="code">/etc/thin/saap.rb</pre>
<pre class="code">cap production deploy
cap production setup:seed_db</pre>
<pre class="code">cap production deploy:start   --&gt;&gt; the first time o do it locally &#039;thin start -C /etc/thin/saap.yml&#039;</pre>

<p>
The deployment process is asking for password to restart the server. Ctrl+C to stop it and do it locally:
</p>
<pre class="code">thin start -C /etc/thin/saap.yml</pre>

<p>
In the production server, to update the crontab (tha cap task is not working because &#039;can not locate Gemfile&#039;
</p>
<pre class="code">bundle exec whenever --update-crontab saap_production --set environment=production --roles=web,app,db</pre>
<pre class="code">bundle exec whenever --clear-crontab saap_production   --&gt; clears the crontab, careful!</pre>

</div>

<h1 class="sectionedit5" id="saapnext_deployments">SAAP: next deployments</h1>
<div class="level1">
<pre class="code">cap production deploy</pre>

<p>
Connect to production server, as su
</p>
<pre class="code">thin restart -C /etc/thin/saap.yml</pre>

<p>
If necessary
</p>
<pre class="code">bundle exec whenever --update-crontab saap_production --set environment=production --roles=web,app,db</pre>

</div>

<h1 class="sectionedit6" id="rollback">Rollback</h1>
<div class="level1">
<pre class="code">cap production deploy:rollback</pre>

</div>

<h1 class="sectionedit7" id="rails_console">Rails console</h1>
<div class="level1">
<pre class="code">bundle exec rails console</pre>

</div>

<h1 class="sectionedit8" id="tutorials">Tutorials</h1>
<div class="level1">

<p>
Unicorn + nginx: <a href="http://sirupsen.com/setting-up-unicorn-with-nginx/" class="urlextern" title="http://sirupsen.com/setting-up-unicorn-with-nginx/"  rel="nofollow">http://sirupsen.com/setting-up-unicorn-with-nginx/</a>
</p>

</div>

<h1 class="sectionedit9" id="code">Code</h1>
<div class="level1">
<pre class="code">thin restart -e production --servers 3 --onebyone --wait 30</pre>

</div>

<h1 class="sectionedit10" id="matar_proceso_server">Matar proceso server</h1>
<div class="level1">
<pre class="code">$ cat tmp/pids/server.pid
=&gt; numero de proceso
$ kill -9 numero_de_proceso</pre>

</div>

<h1 class="sectionedit11" id="create_new_postgres_user_with_password">Create new postgres user with password</h1>
<div class="level1">
<pre class="code">$ sudo -u postgres psql postgres
postgres=# CREATE USER username WITH PASSWORD &#039;password&#039;;
postgres=# GRANT ALL PRIVILEGES ON DATABASE database TO username;
postgres=# ALTER ROLE username WITH SUPERUSER;</pre>

</div>

<h1 class="sectionedit12" id="production_vars">Production vars</h1>
<div class="level1">
<pre class="code">$ RAILS_ENV=production rake secret &gt; clave.txt</pre>

<p>
… add at the end opening the file clave.txt (in vi :r)
</p>
<pre class="code">#!/bin/bash
export RAILS_ENV=production
export RAKE_ENV=production
export SECRET_KEY_BASE=clave
export VAM1_DATABASE_PASSWORD=password</pre>

<p>
In one of these files…
</p>
<pre class="code">$ vi ~/.bash_profile
$ vi ~/.bash_login
$ vi ~/.profile
$ vi ~/.bashrc</pre>

</div>

<h1 class="sectionedit13" id="bash_file_to_start_rails_server">bash file to start rails server</h1>
<div class="level1">

<p>
File name: start_activity_logger.sh
</p>

<p>
Execute with: ./start_activity_logger.sh
</p>
<pre class="code">#!/bin/bash --login
cd ~/projects/activity_logger/
rvm gemset use activity_logger
rails s -p 3001</pre>

<p>
To execute on boot, put it in /etc/init.d and there execute:
</p>
<pre class="code">sudo update-rc.d startactivitylogger.sh defaults</pre>

</div>

<h1 class="sectionedit14" id="nginx_thin">nginx &amp; Thin</h1>
<div class="level1">

<p>
<a href="http://code.macournoyer.com/thin/usage/" class="urlextern" title="http://code.macournoyer.com/thin/usage/"  rel="nofollow">http://code.macournoyer.com/thin/usage/</a><br/>

<a href="https://github.com/macournoyer/thin/" class="urlextern" title="https://github.com/macournoyer/thin/"  rel="nofollow">https://github.com/macournoyer/thin/</a><br/>

<a href="http://jordanhollinger.com/2011/12/19/deploying-with-thin/" class="urlextern" title="http://jordanhollinger.com/2011/12/19/deploying-with-thin/"  rel="nofollow">http://jordanhollinger.com/2011/12/19/deploying-with-thin/</a><br/>

<a href="https://calomel.org/nginx.html" class="urlextern" title="https://calomel.org/nginx.html"  rel="nofollow">https://calomel.org/nginx.html</a><br/>

<a href="http://www.rackspace.com/knowledge_center/article/ubuntu-nginx-rails-and-thin" class="urlextern" title="http://www.rackspace.com/knowledge_center/article/ubuntu-nginx-rails-and-thin"  rel="nofollow">http://www.rackspace.com/knowledge_center/article/ubuntu-nginx-rails-and-thin</a><br/>

<a href="https://coderwall.com/p/ttrhow/deploying-rails-app-using-nginx-puma-and-capistrano-3" class="urlextern" title="https://coderwall.com/p/ttrhow/deploying-rails-app-using-nginx-puma-and-capistrano-3"  rel="nofollow">https://coderwall.com/p/ttrhow/deploying-rails-app-using-nginx-puma-and-capistrano-3</a><br/>

<a href="http://www.gotealeaf.com/blog/deploy-rails-apps-with-capistrano" class="urlextern" title="http://www.gotealeaf.com/blog/deploy-rails-apps-with-capistrano"  rel="nofollow">http://www.gotealeaf.com/blog/deploy-rails-apps-with-capistrano</a><br/>

</p>

</div>

<h2 class="sectionedit15" id="install_thin">Install thin</h2>
<div class="level2">

<p>
<a href="http://www.gotealeaf.com/blog/deploy-rails-apps-with-capistrano" class="urlextern" title="http://www.gotealeaf.com/blog/deploy-rails-apps-with-capistrano"  rel="nofollow">http://www.gotealeaf.com/blog/deploy-rails-apps-with-capistrano</a><br/>

<a href="http://archive.railsforum.com/viewtopic.php?id=17284" class="urlextern" title="http://archive.railsforum.com/viewtopic.php?id=17284"  rel="nofollow">http://archive.railsforum.com/viewtopic.php?id=17284</a><br/>

<a href="http://stackoverflow.com/questions/3230404/rvm-and-thin-root-vs-local-user/3376785#3376785" class="urlextern" title="http://stackoverflow.com/questions/3230404/rvm-and-thin-root-vs-local-user/3376785#3376785"  rel="nofollow">http://stackoverflow.com/questions/3230404/rvm-and-thin-root-vs-local-user/3376785#3376785</a><br/>

<a href="http://articles.slicehost.com/2009/4/17/centos-thin-web-server-for-ruby" class="urlextern" title="http://articles.slicehost.com/2009/4/17/centos-thin-web-server-for-ruby"  rel="nofollow">http://articles.slicehost.com/2009/4/17/centos-thin-web-server-for-ruby</a><br/>

</p>

<p>
Check rvmsudo thin install
</p>

<p>
As root
</p>
<pre class="code">rvm gemset use global -&gt; maybe not necessary nor possible
gem install thin
thin install</pre>
<pre class="code">Installing thin service at /etc/rc.d/thin ...
mkdir -p /etc/rc.d
writing /etc/rc.d/thin
chmod +x /etc/rc.d/thin
mkdir -p /etc/thin</pre>

<p>
If it fails with message <strong>mkmf.rb can&#039;t find header files for ruby at /usr/share/include/ruby.h</strong>
</p>
<pre class="code">sudo yum install ruby-devel (redhat)
sudo apt-get install ruby-dev (debian)</pre>

<p>
After thin install, as the message after installation says, the script &#039;thin&#039; is installed into /etc/rc.d. And <strong>if we want thin to be installed as a service, the script must be put into init.d</strong>. Maybe you can read the scripts under init.d for more information.
</p>
<pre class="code">sudo mv /etc/rc.d/thin /etc/rc.d/init.d/thin
reboot or start service manually</pre>

<p>
To configure thin to start at system boot:
</p>

<p>
on RedHat like systems:
</p>
<pre class="code">sudo /sbin/chkconfig --level 345 thin on</pre>

<p>
on Debian-like systems (Ubuntu):
</p>
<pre class="code">sudo /usr/sbin/update-rc.d -f thin defaults</pre>

<p>
Start service manually
</p>
<pre class="code">service thin start or /etc/init.d/thin start</pre>

<p>
Configuration file sample for app &#039;shk&#039; deployed in ALSER as root:
</p>
<pre class="code">#/etc/thin/shk.yml
---
chdir: &quot;/root/rails_apps/shk/current&quot;
environment: production
address: 0.0.0.0
port: 3000
timeout: 30
log: &quot;/root/log/thin.log&quot;
pid: tmp/pids/thin.pid
max_conns: 1024
max_persistent_conns: 100
rackup: config.ru
require: []
wait: 30
threadpool_size: 20
daemonize: true</pre>

<p>
In Nairobi (thin installed as root)
</p>
<pre class="code">---
chdir: &quot;/home/alfredo/rails_apps/shk/current&quot;
environment: production
address: 0.0.0.0
port: 3010
timeout: 30
log: &quot;/home/alfredo/rails_apps/log/thin.log&quot;
pid: &quot;tmp/pids/thin.pid&quot;
rackup: config.ru
max_conns: 1024
max_persistent_conns: 100
require: []
wait: 30
threadpool_size: 20
daemonize: true</pre>

<p>
If using RVM  
</p>
<pre class="code">rvm wrapper ruby-2.2.0-p0 bootup thin</pre>

<p>
Edit <strong>/etc/init.d/thin</strong>
</p>

<p>
Change DAEMON line by
</p>
<pre class="code">DAEMON=/usr/local/rvm/bin/bootup_thin</pre>

<p>
<strong>For thin config file in project (same config in all stages)</strong><br/>

Create app/config/thin.yml with thin config<br/>

Create symlink (app sharingkitchn deployed with capistrano)
</p>
<pre class="code">ln -s rails_apps/sharingkitchn/current/config/thin.yml /etc/thin/sharingkitchn.yml</pre>

<p>
Commands:
</p>
<pre class="code">/etc/init.d/thin start</pre>

<p>
or
</p>
<pre class="code">service thin start/stop/restart</pre>

<p>
How thin start rails app
</p>
<pre class="code">thin config -C /etc/thin/my-app -c /var/www/my-app/current --servers 1 -e production</pre>

</div>

<h2 class="sectionedit16" id="thin_commands_by_instances_applications">Thin commands by instances (applications)</h2>
<div class="level2">

<p>
1. Set the content of your <strong>/etc/init.d/thin</strong> file to use:
</p>
<pre class="code">#!/bin/sh
### BEGIN INIT INFO
# Provides:          thin
# Required-Start:    $local_fs $remote_fs
# Required-Stop:     $local_fs $remote_fs
# Default-Start:     2 3 4 5
# Default-Stop:      S 0 1 6
# Short-Description: thin initscript
# Description:       thin
### END INIT INFO

# Original author: Forrest Robertson

# Do NOT &quot;set -e&quot;

DAEMON=/usr/local/bin/thin
SCRIPT_NAME=/etc/init.d/thin
CONFIG_PATH=/etc/thin

# Exit if the package is not installed
[ -x &quot;$DAEMON&quot; ] || exit 0

if [ &quot;X$2&quot; = X ] || [ &quot;X$3&quot; = X ]; then
    INSTANCES=&quot;--all $CONFIG_PATH&quot;
else
    INSTANCES=&quot;-C $3&quot;
fi

case &quot;$1&quot; in
  start)
  $DAEMON start $INSTANCES 
  ;;
  stop)
  $DAEMON stop $INSTANCES
  ;;
  restart)
  $DAEMON restart $INSTANCES
  ;;
  *)
  echo &quot;Usage: $SCRIPT_NAME {start|stop|restart} (-C config_file.yml)&quot; &gt;&amp;2
  exit 3
  ;;
esac

:</pre>

<p>
Use <code>thin restart -C /etc/thin/my_website.yml</code>. 
</p>

<p>
Use <code>thin restart</code> (or start or stop, of course) for all instances.
</p>

</div>

<h2 class="sectionedit17" id="nginx_config">nginx config</h2>
<div class="level2">

<p>
/etc/nginx/nginx.conf  – main lines  (see nairobi)
</p>
<pre class="code">user webs;
...
    server {
        client_max_body_size 20M;
        client_body_temp_path /home/alfredo/rails_apps/uploads_temp;
        listen  80;
        server_name  beta.sharingkitchn.com *.beta.sharingkitchn.com;
        root         /home/alfredo/webs/sharingkitchn.com/;

        location / {
                proxy_pass_header Server;
                proxy_temp_path /tmp/nginx 1 2;

                proxy_set_header  X-Real-IP  $remote_addr;
                proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header Host $http_host;
                proxy_redirect off;
                proxy_pass http://localhost:3010;
                break;
                }
        }

</pre>

</div>

<h2 class="sectionedit18" id="nginx_restart">nginx restart</h2>
<div class="level2">
<pre class="code">service nginx restart</pre>

</div>

<h2 class="sectionedit19" id="nginx_start_stop">nginx start/stop</h2>
<div class="level2">

<p>
<a href="http://wiki.nginx.org/CommandLine" class="urlextern" title="http://wiki.nginx.org/CommandLine"  rel="nofollow">http://wiki.nginx.org/CommandLine</a>
</p>

<p>
for starting nginx:
</p>
<pre class="code">  /usr/bin/nginx</pre>

<p>
for stoping nginx:
</p>
<pre class="code">  /usr/bin/nginx -s stop</pre>

</div>

<h2 class="sectionedit20" id="nginx_reload_if_changes_nginxconf">nginx reload if changes nginx.conf</h2>
<div class="level2">
<pre class="code">service nginx reload</pre>

</div>

<h1 class="sectionedit21" id="testing_with_saap_project">Testing with SAAP project</h1>
<div class="level1">

<p>
Bash script: start_saap_server.sh<br/>

Run by: . /start_saap_server.sh
</p>
<pre class="code">#!/bin/bash
. saap_production_vars.sh
cd ~/projects/saap
rvm gemset use saap
thin -C thin.yml start</pre>

<p>
Thin commands: restart stop start
</p>
<pre class="code">thin -C thin.yml restart</pre>

<p>
Ruby script: thin.yml<br/>

Command line to create: thin config -R config.ru -e production -s 1 -O -d -C thin.yml<br/>

See doc for more options: <a href="https://github.com/macournoyer/thin/" class="urlextern" title="https://github.com/macournoyer/thin/"  rel="nofollow">https://github.com/macournoyer/thin/</a>
</p>
<pre class="code">---
chdir: &quot;/home/alfredo/projects/saap&quot;
environment: production
address: 0.0.0.0
port: 3000
timeout: 30
log: log/thin.log
pid: tmp/pids/thin.pid
max_conns: 1024
max_persistent_conns: 100
require: []
wait: 30
threadpool_size: 20
rackup: config.ru
servers: 1
onebyone: true
daemonize: true</pre>

</div>

<h1 class="sectionedit22" id="deploying_rails_app_using_nginx_puma_and_capistrano_3">Deploying Rails app using Nginx, Puma and Capistrano 3</h1>
<div class="level1">

<p>
<a href="https://coderwall.com/p/ttrhow/deploying-rails-app-using-nginx-puma-and-capistrano-3" class="urlextern" title="https://coderwall.com/p/ttrhow/deploying-rails-app-using-nginx-puma-and-capistrano-3"  rel="nofollow">https://coderwall.com/p/ttrhow/deploying-rails-app-using-nginx-puma-and-capistrano-3</a>
</p>

</div>

<h1 class="sectionedit23" id="setting_up_nginx_with_rails">Setting up Nginx with Rails</h1>
<div class="level1">

<p>
<a href="http://www.richgrundy.com/blog/setting-up-nginx-with-rails/" class="urlextern" title="http://www.richgrundy.com/blog/setting-up-nginx-with-rails/"  rel="nofollow">http://www.richgrundy.com/blog/setting-up-nginx-with-rails/</a>
</p>

</div>

<h1 class="sectionedit24" id="staging_server">STAGING server</h1>
<div class="level1">

<p>
<a href="http://emaxime.com/2014/adding-a-staging-environment-to-rails.html" class="urlextern" title="http://emaxime.com/2014/adding-a-staging-environment-to-rails.html"  rel="nofollow">http://emaxime.com/2014/adding-a-staging-environment-to-rails.html</a>
</p>

</div>

<h1 class="sectionedit25" id="views_in_beta">views in beta</h1>
<div class="level1">

<p>
You want to have a new view path in your application. You can create a “app/views/beta” directory, and put your views as if you were in “app/views”.
</p>

<p>
In your ApplicationController, in a before_filter, have your logic do a prepend_view_path “app/views/beta”.
Something like:
</p>
<pre class="code">before_filter :setup_beta</pre>
<pre class="code">def setup_beta
  if request.subdomain == &quot;beta&quot;
    prepend_view_path &quot;app/views/beta&quot;
    # other beta setup
  end
end</pre>

<p>
This way, templates are resolved in “app/views/beta” first, and then, if not found, in “app/views”. Note that, you only have to put in “app/views/beta” the views that differ from those in “app/views”.
</p>

</div>