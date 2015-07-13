---
layout: post
title: "node.js installation"
description: ""
category: [NodeJS, JS]
tags: [NodeJS, JS]
---
{% include JB/setup %}

<h1 class="sectionedit1" id="you_need_to_consider_permissions_during_node_installation">You need to consider permissions during node installation</h1>
<div class="level1">

<p>
<a href="http://stackoverflow.com/questions/16151018/npm-throws-error-without-sudo" class="urlextern" title="http://stackoverflow.com/questions/16151018/npm-throws-error-without-sudo"  rel="nofollow">http://stackoverflow.com/questions/16151018/npm-throws-error-without-sudo</a>
</p>

<p>
(Don&#039;t hack with permissions, install node the right way)
</p>

<p>
Permissions you used when installing node will be required when doing things like writing in your npm directory (npm link, npm install -g, etc.).
</p>

<p>
You probably ran node installation with root permissions, that&#039;s why the global package installation is asking you to be root.
</p>

<p>
There is two ways to manage your node installation:
</p>

<p>
<strong>On a development machine: Install node with NVM (Node Version Manager)</strong>.<a href="https://github.com/creationix/nvm" class="urlextern" title="https://github.com/creationix/nvm"  rel="nofollow">NVM</a><br/>

On a production machine: Install node directly with appropriate permissions.
</p>

<p>
NVM
</p>

<p>
On a development machine, you should not install and run node with root permissions, otherwise things like npm link, npm install -g will need the same permissions.
</p>

<p>
NVM allow you to install node without root permissions and also allow you to install many versions of node to play easily with them.. Perfect for development.
</p>
<ol>
<li class="level1"><div class="li"> Start uninstalling node (root permission will probably be required)<br/>
</div>
</li>
<li class="level1"><div class="li"> Then install NVM following instructions <a href="https://github.com/creationix/nvm" class="urlextern" title="https://github.com/creationix/nvm"  rel="nofollow"> on this page</a>.<br/>
</div>
</li>
<li class="level1"><div class="li"> Install node the proper way: <code>$ nvm install 0.10.35</code> (the last version)<br/>
</div>
</li>
<li class="level1"><div class="li"> Now <strong>npm link</strong>, <strong>npm install -g</strong> will not require you to be root anymore :D</div>
</li>
</ol>

<p>
Directly
</p>

<p>
On a production machine, you can do everything with root permissions. Node installation, packages installations, etc.
</p>

<p>
Run <strong>npm link</strong>, <strong>npm install -g</strong>, etc. with root permissions.
</p>

</div>