---
layout: post
title: "AngularJS"
description: ""
category: [AngularJS, JS, Frameworks]
tags: [AngularJS]
---
{% include JB/setup %}

<h1 class="sectionedit1" id="installation_in_virtual_machine_not_in_shared_folder">Installation in virtual machine NOT in shared folder</h1>
<div class="level1">

<p>
<a href="https://docs.angularjs.org/tutorial" class="urlextern" title="https://docs.angularjs.org/tutorial"  rel="nofollow">https://docs.angularjs.org/tutorial</a><br/>

</p>
<pre class="code">git clone --depth=14 https://github.com/angular/angular-phonecat.git</pre>

<p>
<a href="https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager" class="urlextern" title="https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager"  rel="nofollow">https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager</a>
</p>
<pre class="code">curl -sL https://deb.nodesource.com/setup | sudo bash -
sudo apt-get install -y nodejs</pre>
<pre class="code">sudo curl https://npmjs.org/install.sh | sh
npm --version</pre>

<p>
Como root
</p>
<pre class="code">npm install</pre>

<p>
Start server 
</p>
<pre class="code">npm start</pre>

<p>
Karma Test 
</p>
<pre class="code">npm test</pre>
<pre class="code">sudo npm run update-webdriver</pre>

<p>
End to end test: run protractor test scripts. The app server must be running
</p>
<pre class="code">npm run protractor</pre>

<p>
Driver to test E2E in Firefox<br/>

</p>
<pre class="code">sudo npm install karma-firefox-launcher --save-dev</pre>

<p>
Selenium Webdriver manager
</p>
<pre class="code">webdriver-manager status</pre>

</div>

<h1 class="sectionedit1" id="yeoman_generator">Yeoman generator</h1>
<div class="level1">

<p>
<a href="http://yeoman.io/" class="urlextern" title="http://yeoman.io/"  rel="nofollow">http://yeoman.io/</a><br/>

</p>

<p>
<a href="https://github.com/yeoman/generator-angular" class="urlextern" title="https://github.com/yeoman/generator-angular"  rel="nofollow">https://github.com/yeoman/generator-angular</a><br/>

</p>

<p>
<a href="https://github.com/cgross/generator-cg-angular" class="urlextern" title="https://github.com/cgross/generator-cg-angular"  rel="nofollow">https://github.com/cgross/generator-cg-angular</a>
</p>

</div>
