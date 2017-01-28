---
layout: post
title: "Ruby, Node, Rails on Ubuntu 14.04"
description: ""
category: [installation]
tags: []
---
{% include JB/setup %}

<div id="dw__toc">
<h3 class="toggle">Table of Contents</h3>
<div>

<ul class="toc">
<li class="level1"><div class="li"><a href="#new_installation_ruby_nodejs_rails">New installation Ruby, NodeJS &amp; Rails</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#install_ruby_on_ubuntu_using_rbenv">Install Ruby on Ubuntu using rbenv</a></div></li>
<li class="level2"><div class="li"><a href="#configuring_git">Configuring GIT</a></div></li>
<li class="level2"><div class="li"><a href="#installing_nodejs_rails">Installing NodeJS &amp; Rails</a></div></li>
<li class="level2"><div class="li"><a href="#setting_up_postgresql">Setting Up PostgreSQL</a></div></li>
<li class="level2"><div class="li"><a href="#final_stepscheck_the_installation">Final Steps :: check the installation</a></div></li>
<li class="level2"><div class="li"><a href="#issue_on_installing_node_npm_as_sudo_and_other_packages_with_no_sudo">Issue on installing node&amp;npm as sudo and other packages with no sudo</a></div></li>
<li class="level2"><div class="li"><a href="#more_about_postgresql">More about PostgreSQL</a></div></li>
<li class="level2"><div class="li"><a href="#rails_app_filedatabaseyml">Rails app file :: database.yml</a></div></li>
<li class="level2"><div class="li"><a href="#create_the_databases">Create the databases</a></div></li>
</ul></li>
</ul>
</div>
</div>
<!-- TOC END -->

<h1 class="sectionedit1" id="new_installation_ruby_nodejs_rails">New installation Ruby, NodeJS &amp; Rails</h1>
<div class="level1">

<p>
Another source link: <a href="http://www.gotealeaf.com/blog/how-to-install-ruby-on-rails-development-environment-for-linux" class="urlextern" title="http://www.gotealeaf.com/blog/how-to-install-ruby-on-rails-development-environment-for-linux"  rel="nofollow">http://www.gotealeaf.com/blog/how-to-install-ruby-on-rails-development-environment-for-linux</a>
</p>

</div>

<h2 class="sectionedit2" id="install_ruby_on_ubuntu_using_rbenv">Install Ruby on Ubuntu using rbenv</h2>
<div class="level2">

<p>
<a href="https://gorails.com/setup/ubuntu/14.04" class="urlextern" title="https://gorails.com/setup/ubuntu/14.04"  rel="nofollow">https://gorails.com/setup/ubuntu/14.04</a><br/>

</p>
<pre class="code">sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties

cd
git clone git://github.com/sstephenson/rbenv.git .rbenv
echo &#039;export PATH=&quot;$HOME/.rbenv/bin:$PATH&quot;&#039; &gt;&gt; ~/.bashrc
echo &#039;eval &quot;$(rbenv init -)&quot;&#039; &gt;&gt; ~/.bashrc
exec $SHELL

git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
echo &#039;export PATH=&quot;$HOME/.rbenv/plugins/ruby-build/bin:$PATH&quot;&#039; &gt;&gt; ~/.bashrc
exec $SHELL

rbenv install 2.1.3
rbenv global 2.1.3
ruby -v</pre>

<p>
The last step is to tell Rubygems not to install the documentation for each package locally
</p>
<pre class="code">echo &quot;gem: --no-ri --no-rdoc&quot; &gt; ~/.gemrc</pre>

</div>

<h2 class="sectionedit3" id="configuring_git">Configuring GIT</h2>
<div class="level2">
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

<h2 class="sectionedit4" id="installing_nodejs_rails">Installing NodeJS &amp; Rails</h2>
<div class="level2">
<pre class="code">sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install nodejs
gem install rails</pre>

<p>
If you&#039;re using rbenv, you&#039;ll need to run the following command to make the rails executable available:
</p>
<pre class="code">rbenv rehash</pre>

<p>
Now that you&#039;ve installed Rails, you can run the rails -v command to make sure you have everything installed correctly:
</p>
<pre class="code">rails -v
# Rails 4.1.8 o similar</pre>

</div>

<h2 class="sectionedit5" id="setting_up_postgresql">Setting Up PostgreSQL</h2>
<div class="level2">

<p>
For PostgreSQL, we&#039;re going to add a new repository to easily install a recent version of Postgres 9.3.
</p>
<pre class="code">sudo sh -c &quot;echo &#039;deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main&#039; &gt; /etc/apt/sources.list.d/pgdg.list&quot;
wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install postgresql-common
sudo apt-get install postgresql-9.3 libpq-dev</pre>

<p>
The postgres installation doesn&#039;t setup a user for you, so you&#039;ll need to follow these steps to create a user with permission to create databases. 
</p>
<pre class="code">sudo -u postgres createuser alfredo -s</pre>

<p>
# If you would like to set a password for the user, you can do the following
</p>
<pre class="code">sudo -u postgres psql
postgres=# \password alfredo</pre>

</div>

<h2 class="sectionedit6" id="final_stepscheck_the_installation">Final Steps :: check the installation</h2>
<div class="level2">

<p>
And now for the moment of truth. Let&#039;s create your first Rails application:
</p>

<p>
#### If you want to use Postgres<br/>

# Note that this will expect a postgres user with the same username<br/>

# as your app, you may need to edit config/database.yml to match the<br/>

# user you created earlier<br/>

</p>
<pre class="code">rails new myapp -d postgresql</pre>

<p>
# Move into the application directory
</p>
<pre class="code">cd myapp</pre>

<p>
# If you setup MySQL or Postgres with a username/password, modify the<br/>

# config/database.yml file to contain the username/password that you specified<br/>

</p>

<p>
# Create the database
</p>
<pre class="code">rake db:create
rails server</pre>

</div>

<h2 class="sectionedit7" id="issue_on_installing_node_npm_as_sudo_and_other_packages_with_no_sudo">Issue on installing node&amp;npm as sudo and other packages with no sudo</h2>
<div class="level2">

<p>
<a href="http://stackoverflow.com/questions/16151018/npm-throws-error-without-sudo" class="urlextern" title="http://stackoverflow.com/questions/16151018/npm-throws-error-without-sudo"  rel="nofollow">http://stackoverflow.com/questions/16151018/npm-throws-error-without-sudo</a>
</p>

<p>
It&#039;s safer to create a new group for node-users and add the required users to this group, further to set the ownership of node-dependant files/directories to this group.
</p>

<p>
# Create new group
</p>
<pre class="code">sudo groupadd nodegrp </pre>

<p>
# Add user to group (logname is a variable and gets replaced by the currently logged in user)
</p>
<pre class="code">sudo usermod -a -G nodegrp `logname`</pre>

<p>
# Instant access to group without re-login
</p>
<pre class="code">newgrp nodegrp</pre>

<p>
# Check group - nodegrp should be listed as well now
</p>
<pre class="code">groups</pre>

<p>
# Change group of node_modules, node, npm to new group 
</p>
<pre class="code">sudo chgrp -R nodegrp /usr/lib/node_modules/
sudo chgrp -R nodegrp /usr/lib/nodejs
sudo chgrp nodegrp /usr/bin/node
sudo chgrp nodegrp /usr/bin/npm
</pre>

<p>
# (You may want to change a couple of more files (like grunt etc) in your /usr/bin/ directory.)<br/>

</p>

<p>
Now you can easily install your modules as user
</p>
<pre class="code">npm install -g generator-angular</pre>

<p>
<strong>Some modules (grunt, bower, yo etc.) will still need to be installed as root. This is because they create symlinks in /user/bin/.</strong>
</p>

</div>

<h2 class="sectionedit8" id="more_about_postgresql">More about PostgreSQL</h2>
<div class="level2">

<p>
basename=# SELECT * FROM tabla; <br/>

</p>

<p>
SHOW TABLES     basename=# \d<br/>

SHOW DATABASES  basename=# \l<br/>

SHOW COLUMNS    basename=# \d table<br/>

DESCRIBE TABLE  basename=# \d+ table<br/>

\du lista los usuarios de postgres y sus propiedades<br/>

createuser -P -s -d -r -e zabbix crea el usuario zabbix con privilegios de root<br/>

psql -h localhost -U zabbix zabbix entramos en Postgres, con el usuario zabbix a la base de datos zabbix<br/>

</p>

<p>
<strong>Conectar a base de datos</strong> # \c basename<br/>

</p>

<p>
<strong>Cómo revisar si PostgreSQL está funcionando:</strong> $ /etc/init.d/postgresql status Password:
</p>
<pre class="code">==&gt; pg_ctl: server is running (PID: 6171)</pre>

<p>
Salir                    # \q<br/>

</p>

</div>

<h2 class="sectionedit9" id="rails_app_filedatabaseyml">Rails app file :: database.yml</h2>
<div class="level2">

<p>
development:
</p>
<pre class="code">adapter: postgresql
encoding: unicode
database: myapp_development
pool: 5
username: alfredo
password: oderfla</pre>

<p>
test:
</p>
<pre class="code">adapter: postgresql
encoding: unicode
database: myapp_test
pool: 5
username: alfredo
password: oderfla</pre>

</div>

<h2 class="sectionedit10" id="create_the_databases">Create the databases</h2>
<div class="level2">

<p>
<code>$ rake db:create:all</code><br/>

</p>

</div>