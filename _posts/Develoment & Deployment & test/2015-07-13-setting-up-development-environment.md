---
layout: post
title: "Setting up development environment"
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
<li class="level1"><div class="li"><a href="#railsgirls_installation_scripts">RailsGirls installation scripts</a></div></li>
<li class="level1"><div class="li"><a href="#nodejs_and_npm">NodeJS and npm</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#test_node_installation">Test node installation</a></div></li>
</ul>
</li>
<li class="level1"><div class="li"><a href="#production_server_with_unicorn_nginx">Production server with Unicorn &amp; nginx</a></div></li>
<li class="level1"><div class="li"><a href="#uninstall_rvm">Uninstall RVM</a></div></li>
<li class="level1"><div class="li"><a href="#install_rvm_ruby">Install RVM &amp; Ruby</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#upgrade_rvm">Upgrade rvm</a></div>
<ul class="toc">
<li class="level3"><div class="li"><a href="#integrating_rvm_with_gnome-terminal">Integrating RVM with Gnome-terminal</a></div></li>
<li class="level3"><div class="li"><a href="#recomended_install_gem_nokogiri_rails_install_nokogiri">Recomended install gem nokogiri (Rails install Nokogiri)</a></div></li>
</ul>
</li>
<li class="level2"><div class="li"><a href="#rails">Rails</a></div></li>
<li class="level2"><div class="li"><a href="#gemsets">Gemsets</a></div>
<ul class="toc">
<li class="level3"><div class="li"><a href="#create_configurations_files_ruby-version_ruby-gemset">Create configurations files .ruby-version &amp; .ruby-gemset</a></div></li>
</ul>
</li>
</ul>
</li>
<li class="level1"><div class="li"><a href="#postgres_gem_in_fedora">Postgres gem in fedora</a></div></li>
<li class="level1"><div class="li"><a href="#updating_an_existing_app">Updating an existing app</a></div></li>
<li class="level1"><div class="li"><a href="#update_gems">Update GEMs</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#update_only_one_gem">Update only one gem</a></div></li>
<li class="level2"><div class="li"><a href="#update_one_gem_and_its_dependencies">Update one gem and its dependencies</a></div></li>
<li class="level2"><div class="li"><a href="#update_everthing">Update everthing</a></div></li>
</ul>
</li>
<li class="level1"><div class="li"><a href="#git">GIT</a></div></li>
<li class="level1"><div class="li"><a href="#installing_postgresql_server_locally_--_ubuntu">Installing PostgreSQL Server locally -- ubuntu</a></div></li>
<li class="level1"><div class="li"><a href="#create_new_postrges_user_with_password">Create new postrges user with password</a></div></li>
<li class="level1"><div class="li"><a href="#install_postresql_--_fedora">Install postreSQL -- fedora</a></div></li>
<li class="level1"><div class="li"><a href="#postgres_en_fedora_20">Postgres en Fedora 20</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#to_make_pg_start_on_system_boot">to make pg start on system boot:</a></div></li>
<li class="level2"><div class="li"><a href="#failed_to_build_gem_native_extension_installing_postgres">Failed to build gem native extension installing postgres</a></div></li>
</ul>
</li>
<li class="level1"><div class="li"><a href="#start_stop_postgres_---_fedora">Start/stop postgres  --- fedora</a></div></li>
<li class="level1"><div class="li"><a href="#postgres_service_control">Postgres Service control</a></div></li>
<li class="level1"><div class="li"><a href="#reset_password">Reset password</a></div></li>
<li class="level1"><div class="li"><a href="#full_removal_of_postgres">Full removal of Postgres</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#pg_ctl">pg_ctl</a></div></li>
<li class="level2"><div class="li"><a href="#postgres_errors">Postgres Errors</a></div></li>
</ul>
</li>
<li class="level1"><div class="li"><a href="#environment_vars">Environment vars</a></div></li>
<li class="level1"><div class="li"><a href="#production_env_vars">Production env vars</a></div></li>
<li class="level1"><div class="li"><a href="#start_rails_server">Start rails server</a></div></li>
<li class="level1"><div class="li"><a href="#production_secret_key_base_generation">production secret_key_base generation</a></div></li>
<li class="level1"><div class="li"><a href="#bower">Bower</a></div></li>
<li class="level1"><div class="li"><a href="#bash_file_to_start_rails_server">bash file to start rails server</a></div></li>
</ul>
</div>
</div>
<!-- TOC END -->

<h1 class="sectionedit1" id="railsgirls_installation_scripts">RailsGirls installation scripts</h1>
<div class="level1">

<p>
See: <a href="https://github.com/railsgirls/installation-scripts" class="urlextern" title="https://github.com/railsgirls/installation-scripts"  rel="nofollow">https://github.com/railsgirls/installation-scripts</a><br/>

</p>

</div>

<h1 class="sectionedit2" id="nodejs_and_npm">NodeJS and npm</h1>
<div class="level1">

<p>
Install Node via NVM.
See: <a href="/wikimemo/doku.php?id=nodejs" class="wikilink1" title="nodejs">NodeJS  proper installation</a><br/>

</p>
<pre class="code">$ curl https://raw.githubusercontent.com/creationix/nvm/v0.22.2/install.sh | bash</pre>

<p>
Restart terminal shell
</p>
<pre class="code">$ nvm install 0.10   --or -- nvm install stable</pre>

<p>
To use NodeJS
</p>
<pre class="code">$ nvm use stable</pre>

<p>
To set a default Node version to be used in any new shell, use the alias &#039;default&#039;:
</p>
<pre class="code">$ nvm alias default stable</pre>

</div>

<h2 class="sectionedit3" id="test_node_installation">Test node installation</h2>
<div class="level2">
<pre class="code">// hello_node.js
var http = require(&#039;http&#039;);
http.createServer(function (req, res) {
  res.writeHead(200, {&#039;Content-Type&#039;: &#039;text/plain&#039;});
  res.end(&#039;Hello Node.js\n&#039;);
}).listen(8124, &quot;127.0.0.1&quot;);
console.log(&#039;Server running at http://127.0.0.1:8124/&#039;);</pre>

</div>

<h1 class="sectionedit4" id="production_server_with_unicorn_nginx">Production server with Unicorn &amp; nginx</h1>
<div class="level1">

<p>
<a href="http://www.gotealeaf.com/blog/setting-up-your-production-server-with-nginx-and-unicorn" class="urlextern" title="http://www.gotealeaf.com/blog/setting-up-your-production-server-with-nginx-and-unicorn"  rel="nofollow">http://www.gotealeaf.com/blog/setting-up-your-production-server-with-nginx-and-unicorn</a>
</p>

</div>

<h1 class="sectionedit5" id="uninstall_rvm">Uninstall RVM</h1>
<div class="level1">
<pre class="code">sudo rvm implode
sudo rm -rf /etc/rvmrc /etc/profile.d/rvm.sh /usr/local/rvm</pre>

</div>

<h1 class="sectionedit6" id="install_rvm_ruby">Install RVM &amp; Ruby</h1>
<div class="level1">

<p>
Add user to sudoers list    
</p>
<pre class="code">  usermod -a -G wheel alfredo
  =&gt; alfredo is sudoer</pre>

<p>
rvm ⇒ ver instrucciones en <a href="https://rvm.io/" class="urlextern" title="https://rvm.io/"  rel="nofollow">https://rvm.io/</a>
</p>

<p>
Source: <a href="http://railsapps.github.io/installrubyonrails-ubuntu.html" class="urlextern" title="http://railsapps.github.io/installrubyonrails-ubuntu.html"  rel="nofollow">http://railsapps.github.io/installrubyonrails-ubuntu.html</a><br/>

</p>
<pre class="code">$ \curl -L https://get.rvm.io | bash -s stable --ruby</pre>

<p>
If it fails, follow the given instruction to download keys and try again.
</p>

<p>
Reopen terminal shell.
</p>

<p>
Generate ri documentation (recomended)
</p>
<pre class="code">$ rvm docs generate-ri</pre>

<p>
<a href="https://coderwall.com/p/ttrhow/deploying-rails-app-using-nginx-puma-and-capistrano-3" class="urlextern" title="https://coderwall.com/p/ttrhow/deploying-rails-app-using-nginx-puma-and-capistrano-3"  rel="nofollow">https://coderwall.com/p/ttrhow/deploying-rails-app-using-nginx-puma-and-capistrano-3</a>
Install rvm, ruby and rubygems:
</p>
<pre class="code">curl -L get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm requirements
rvm install 2.1.0
rvm use 2.1.0 --default
rvm rubygems current</pre>

</div>

<h2 class="sectionedit7" id="upgrade_rvm">Upgrade rvm</h2>
<div class="level2">
<pre class="code">rvm get head</pre>

</div>

<h3 class="sectionedit8" id="integrating_rvm_with_gnome-terminal">Integrating RVM with Gnome-terminal</h3>
<div class="level3">

<p>
For RVM to work properly, you have to check the <strong>&#039;Run command as login shell&#039; checkbox</strong> on the Title and Command tab of gnome-terminal&#039;s Edit ▸ Profile Preferences menu dialog, in case the menu is missing right click the terminal app and navigate Profiles ▸ Profile Preferences.
</p>

</div>

<h3 class="sectionedit9" id="recomended_install_gem_nokogiri_rails_install_nokogiri">Recomended install gem nokogiri (Rails install Nokogiri)</h3>
<div class="level3">

<p>
This is a basic gem that many others depend on and it takes time to install it. So, it&#039;s recomended install it in advance in the global gemset:
</p>
<pre class="code">$ gem install nokogiri</pre>

</div>

<h2 class="sectionedit10" id="rails">Rails</h2>
<div class="level2">
<pre class="code">$ gem install rails</pre>

</div>

<h2 class="sectionedit11" id="gemsets">Gemsets</h2>
<div class="level2">

<p>
Create new gemset for the application
</p>
<pre class="code">rvm gemset create &lt;appname&gt;
rvm gemset use &lt;appname&gt;</pre>

<p>
Remove gemset:
</p>
<pre class="code">rvm gemset delete &lt;name&gt;</pre>

<p>
It is a good idea to use RVM, the Ruby Version Manager, and create a project-specific rvm gemset.
</p>
<pre class="code">$ rvm gemset list
$ rvm gemset use global</pre>

<p>
To list the gems installed by RVM:
</p>
<pre class="code">rvm all do gem list
rvm &lt;ruby version&gt; do gem list</pre>

<p>
To list the gems installed by bundle in the application:
</p>
<pre class="code">bundle list</pre>

</div>

<h3 class="sectionedit12" id="create_configurations_files_ruby-version_ruby-gemset">Create configurations files .ruby-version &amp; .ruby-gemset</h3>
<div class="level3">

<p>
Source: <a href="https://rvm.io/workflow/projects#project-file-ruby-version" class="urlextern" title="https://rvm.io/workflow/projects#project-file-ruby-version"  rel="nofollow">https://rvm.io/workflow/projects#project-file-ruby-version</a>
</p>

<p>
To create both files in the project folder:
</p>
<pre class="code">$ rvm --ruby-version use 2.2.0@my_app --create</pre>

<p>
Use the corresponding Ruby versión and app name. Append –create if the gems doesn&#039;t exist yet.
</p>

</div>

<h1 class="sectionedit13" id="postgres_gem_in_fedora">Postgres gem in fedora</h1>
<div class="level1">
<pre class="code">Gem::Ext::BuildError: ERROR: Failed to build gem native extension.</pre>
<pre class="code">yum install /usr/include/libpq-fe.h</pre>

</div>

<h1 class="sectionedit14" id="updating_an_existing_app">Updating an existing app</h1>
<div class="level1">
<ol>
<li class="level1"><div class="li"> Create .ruby-version and .ruby-gemset files</div>
</li>
<li class="level1"><div class="li"> Change Ruby versión in Gemfile</div>
</li>
<li class="level1"><div class="li"> Bundle update</div>
</li>
</ol>

</div>

<h1 class="sectionedit15" id="update_gems">Update GEMs</h1>
<div class="level1">

<p>
Source: <a href="http://ilikestuffblog.com/2012/07/01/you-should-update-one-gem-at-a-time-with-bundler-heres-how/" class="urlextern" title="http://ilikestuffblog.com/2012/07/01/you-should-update-one-gem-at-a-time-with-bundler-heres-how/"  rel="nofollow">http://ilikestuffblog.com/2012/07/01/you-should-update-one-gem-at-a-time-with-bundler-heres-how/</a><br/>

</p>

</div>

<h2 class="sectionedit16" id="update_only_one_gem">Update only one gem</h2>
<div class="level2">
<pre class="code">bundle update ––source gemname</pre>

</div>

<h2 class="sectionedit17" id="update_one_gem_and_its_dependencies">Update one gem and its dependencies</h2>
<div class="level2">
<pre class="code">bundle update gemname</pre>

</div>

<h2 class="sectionedit18" id="update_everthing">Update everthing</h2>
<div class="level2">
<pre class="code">bundle update</pre>

</div>

<h1 class="sectionedit19" id="git">GIT</h1>
<div class="level1">
<pre class="code">git config --global color.ui true
git config --global user.name &quot;Alfredo&quot;
git config --global user.email &quot;alfredo.roca.mas@gmail.com&quot;
ssh-keygen -t rsa -C &quot;alfredo.roca.mas@gmail.com&quot;</pre>

<p>
The next step is to take the newly generated SSH key and add it to your Github account. You want to copy and paste the output of the following command and paste it <a href="https://github.com/settings/ssh" class="urlextern" title="https://github.com/settings/ssh"  rel="nofollow">here</a>.
</p>
<pre class="code">cat ~/.ssh/id_rsa.pub</pre>

<p>
Once you&#039;ve done this, you can check and see if it worked:
</p>
<pre class="code">ssh -T git@github.com</pre>

<p>
You should get a message like this:
</p>

<p>
<em>Hi excid3! You&#039;ve successfully authenticated, but GitHub does not provide shell access.</em>
</p>

</div>

<h1 class="sectionedit20" id="installing_postgresql_server_locally_--_ubuntu">Installing PostgreSQL Server locally -- ubuntu</h1>
<div class="level1">

<p>
Source: <a href="https://help.ubuntu.com/community/PostgreSQL" class="urlextern" title="https://help.ubuntu.com/community/PostgreSQL"  rel="nofollow">https://help.ubuntu.com/community/PostgreSQL</a><br/>

</p>
<pre class="code">sudo apt-get install postgresql postgresql-contrib
sudo apt-get install pgadmin3
sudo -u postgres psql postgres
# \password postgres  --&gt; enter password for user postgres
sudo -u postgres psql
# CREATE EXTENSION adminpack;</pre>

<p>
Edit pg_hba.conf … Ask pg where the file is…
</p>
<pre class="code">postgres=# show hba_file;
              hba_file               
-------------------------------------
 /var/lib/pgsql/9.4/data/pg_hba.conf
(1 row)
</pre>

<p>
… change method peer by md5
</p>
<pre class="code"># Database administrative login by Unix domain socket
local   all             postgres                                md5</pre>
<pre class="code">sudo /etc/init.d/postgresql reload</pre>

</div>

<h1 class="sectionedit21" id="create_new_postrges_user_with_password">Create new postrges user with password</h1>
<div class="level1">
<pre class="code">$ sudo -u postgres psql postgres
postgres=# CREATE USER username WITH PASSWORD &#039;password&#039;;
postgres=# GRANT ALL PRIVILEGES ON DATABASE database TO username;
postgres=# ALTER ROLE username WITH SUPERUSER CREATEDB;</pre>

<p>
See also: <br/>

<a href="http://technobytz.com/install-postgresql-9-3-ubuntu.html" class="urlextern" title="http://technobytz.com/install-postgresql-9-3-ubuntu.html"  rel="nofollow">http://technobytz.com/install-postgresql-9-3-ubuntu.html</a><br/>

</p>

</div>

<h1 class="sectionedit22" id="install_postresql_--_fedora">Install postreSQL -- fedora</h1>
<div class="level1">

<p>
<a href="https://fedoraproject.org/wiki/PostgreSQL#Installation" class="urlextern" title="https://fedoraproject.org/wiki/PostgreSQL#Installation"  rel="nofollow">https://fedoraproject.org/wiki/PostgreSQL#Installation</a>
</p>

</div>

<h1 class="sectionedit23" id="postgres_en_fedora_20">Postgres en Fedora 20</h1>
<div class="level1">

<p>
Date: 28/2/2015
</p>

<p>
<a href="https://wiki.postgresql.org/wiki/YUM_Installation" class="urlextern" title="https://wiki.postgresql.org/wiki/YUM_Installation"  rel="nofollow">https://wiki.postgresql.org/wiki/YUM_Installation</a>
</p>

<p>
como root
</p>
<pre class="code">  yum localinstall http://yum.postgresql.org/9.4/fedora/fedora-20-i686/pgdg-fedora94-9.4-1.noarch.rpm  
  (esto no sé para qué es)</pre>
<pre class="code">  yum install postgresql94-server</pre>
<pre class="code">  yum install postgresql94-devel</pre>

<p>
Alternative - with database initialization:
</p>

<p>
<a href="https://fedoraproject.org/wiki/PostgreSQL" class="urlextern" title="https://fedoraproject.org/wiki/PostgreSQL"  rel="nofollow">https://fedoraproject.org/wiki/PostgreSQL</a>:
</p>
<pre class="code">  sudo yum install postgresql94-server postgresql94-contrib
  sudo /usr/pgsql-9.4/bin/postgresql94-setup initdb</pre>

<p>
In .bash_profile add
</p>
<pre class="code">  export PGHOST=localhost</pre>

</div>

<h2 class="sectionedit24" id="to_make_pg_start_on_system_boot">to make pg start on system boot:</h2>
<div class="level2">
<pre class="code">  sudo chkconfig postgresql-9.4 on</pre>

</div>

<h2 class="sectionedit25" id="failed_to_build_gem_native_extension_installing_postgres">Failed to build gem native extension installing postgres</h2>
<div class="level2">

<p>
If bundle install and gem install pg -v &#039;0.18.1&#039; raises ERROR: <strong>Failed to build gem native extension  …. Cannot find pg_config file</strong>
</p>
<pre class="code">  gem install pg -- --with-pg-config=/usr/pgsql-9.4/bin/pg_config</pre>

<p>
Problem:
bundling cloned app:
</p>

<p>
ERROR: Failed to build gem native extension.
checking for pg_config… no
No pg_config… trying anyway. If building fails, please try again with
 –with-pg-config=/path/to/pg_config
checking for libpq-fe.h… no
<strong>Can&#039;t find the &#039;libpq-fe.h header</strong>
</p>

<p>
Solution:
</p>
<pre class="code">  bundle config build.pg --with-pg-config=/usr/pgsql-9.4/bin/pg_config</pre>

</div>

<h1 class="sectionedit26" id="start_stop_postgres_---_fedora">Start/stop postgres  --- fedora</h1>
<div class="level1">
<pre class="code">sudo /bin/systmctl start/stop postgresql</pre>

</div>

<h1 class="sectionedit27" id="postgres_service_control">Postgres Service control</h1>
<div class="level1">

<p>
To control the database service, use:
</p>
<pre class="code">  service postgresql-9.4 &lt;command&gt;</pre>

<p>
where &lt;command&gt; can be:
</p>
<pre class="code">  start : start the database
  stop : stop the database
  restart : stop/start the database; used to read changes to core configuration files
  reload : reload pg_hba.conf file while keeping database running </pre>
<pre class="code">  sudo service postgresql-9.4 start</pre>

</div>

<h1 class="sectionedit28" id="reset_password">Reset password</h1>
<div class="level1">

<p>
Edit pg_hba.conf
en ubuntu: sudo nano /etc/postgresql/9.3/main/pg_hba.conf
en fedora: /var/lib/pgsql/data/pg_hba.conf
change or add line …
</p>
<pre class="code">local all postgres  trust sameuser</pre>

<p>
Restart postgres
</p>
<pre class="code">/etc/init.d/postgresql-8.3 restart</pre>

</div>

<h1 class="sectionedit29" id="full_removal_of_postgres">Full removal of Postgres</h1>
<div class="level1">
<pre class="code">sudo apt-get --purge remove postgresql\*
sudo apt-get remove pgadmin3
sudo rm -rf /etc/postgresql/
sudo rm -r /etc/postgresql-common/
sudo rm -r /var/lib/postgresql/
sudo userdel -r postgres
sudo groupdel postgres</pre>

</div>

<h2 class="sectionedit30" id="pg_ctl">pg_ctl</h2>
<div class="level2">

<p>
Source: <a href="http://www.postgresql.org/docs/9.1/static/app-pg-ctl.html" class="urlextern" title="http://www.postgresql.org/docs/9.1/static/app-pg-ctl.html"  rel="nofollow">http://www.postgresql.org/docs/9.1/static/app-pg-ctl.html</a>
</p>
<pre class="code">/usr/lib/postgresql/9.4/bin/pg_ctl start -D data_directory</pre>
<pre class="code">/usr/lib/postgresql/9.4/bin/pg_ctl stop</pre>
<pre class="code">/usr/lib/postgresql/9.4/bin/pg_ctl restart -D data_directory</pre>

<p>
Query for data directory:
</p>
<pre class="code">postgres=# SHOW data_directory;
=&gt;        data_directory        
------------------------------
 /var/lib/postgresql/9.4/main</pre>
<pre class="code">postgres=# select setting from pg_settings where name = &#039;data_directory&#039;;</pre>

</div>

<h2 class="sectionedit31" id="postgres_errors">Postgres Errors</h2>
<div class="level2">

<p>
Error messages:
</p>

<p>
User not found in pg_hba.conf
</p>
<pre class="code">  psql: FATAL:  no pg_hba.conf entry for host &quot;[local]&quot;, user &quot;couling&quot;, database &quot;main&quot;, SSL off</pre>

<p>
User failed password auth:
</p>
<pre class="code">  psql: FATAL:  password authentication failed for user &quot;couling&quot;</pre>

<p>
Missing unix socket file:
</p>
<pre class="code">  psql: could not connect to server: No such file or directory
    Is the server running locally and accepting
    connections on Unix domain socket &quot;/var/run/postgresql/.s.PGSQL.5432&quot;?</pre>

<p>
Unix socket exists, but server not listening to it.
</p>
<pre class="code">  psql: could not connect to server: Connection refused
    Is the server running locally and accepting
    connections on Unix domain socket &quot;/var/run/postgresql/.s.PGSQL.5432&quot;?</pre>

<p>
Bad file permissions on unix socket file:
</p>
<pre class="code">  psql: could not connect to server: Permission denied
    Is the server running locally and accepting
    connections on Unix domain socket &quot;/var/run/postgresql/.s.PGSQL.5432&quot;?
  </pre>

</div>

<h1 class="sectionedit32" id="environment_vars">Environment vars</h1>
<div class="level1">
<pre class="code">$ export KEY=value
&gt; ENV[&quot;KEY&quot;] =&gt; &quot;value&quot;</pre>

</div>

<h1 class="sectionedit33" id="production_env_vars">Production env vars</h1>
<div class="level1">

<p>
RAILS_ENV=production
</p>

<p>
RAKE_ENV=production
</p>

<p>
SECRET_KEY_BASE=    (see below)
</p>

<p>
APP_DATABASE_PASSWORD=
</p>
<pre class="code">bundle exec rake db:version</pre>

<p>
<strong>Carrierwave in production:</strong>
</p>
<pre class="code">config.serve_static_assets = true</pre>

</div>

<h1 class="sectionedit34" id="start_rails_server">Start rails server</h1>
<div class="level1">
<pre class="code">APP_DATABASE_PASSWORD=password rails s -b 127.0.0.1 -p 3000</pre>

</div>

<h1 class="sectionedit35" id="production_secret_key_base_generation">production secret_key_base generation</h1>
<div class="level1">

<p>
<a href="http://stackoverflow.com/questions/23180650/how-to-solve-error-missing-secret-key-base-for-production-environment-on-h" class="urlextern" title="http://stackoverflow.com/questions/23180650/how-to-solve-error-missing-secret-key-base-for-production-environment-on-h"  rel="nofollow">http://stackoverflow.com/questions/23180650/how-to-solve-error-missing-secret-key-base-for-production-environment-on-h</a>
</p>
<pre class="code">$ RAILS_ENV=production rake secret &gt; clave.txt</pre>

<p>
In one of these files…
</p>
<pre class="code">$ vi ~/.bash_profile
$ vi ~/.bash_login
$ vi ~/.profile</pre>

<p>
… add at the end opening the file clave.txt (in vi :r)
</p>
<pre class="code">export SECRET_KEY_BASE=clave</pre>

<p>
Restart console to check:
</p>
<pre class="code">$ echo $SECRET_KEY_BASE</pre>

</div>

<h1 class="sectionedit36" id="bower">Bower</h1>
<div class="level1">
<pre class="code">npm install -g bower</pre>

</div>

<h1 class="sectionedit37" id="bash_file_to_start_rails_server">bash file to start rails server</h1>
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