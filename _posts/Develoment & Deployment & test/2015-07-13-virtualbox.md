---
layout: post
title: "VirtualBox"
description: ""
category: [virtualbox]
tags: []
---
{% include JB/setup %}
<!-- TOC START -->
<div id="dw__toc">
  <h3 class="toggle">Table of Contents</h3>
  <div>

    <ul class="toc">
      <li class="level1"><div class="li"><a href="#virtualbox_shared_folders_path">VirtualBox shared folders path</a></div></li>
      <li class="level1"><div class="li"><a href="#increase_hdd_size_in_virtualbox_machine">Increase HDD size in VirtualBox machine</a></div></li>
      <li class="level1"><div class="li"><a href="#how_to_size_monitor_to_maximum_resolution">How to size monitor to maximum resolution</a></div></li>
      <li class="level1"><div class="li"><a href="#how_to_enable_root_login">How to enable root login?</a></div></li>
      <li class="level1"><div class="li"><a href="#javascript_runtime">Javascript runtime</a></div>
        <ul class="toc">
          <li class="level2"><div class="li"><a href="#bowerfrontend_package_manager">Bower: frontend package manager</a></div></li>
        </ul>
      </li>
      <li class="level1"><div class="li"><a href="#git_remember_credential_temporaly">GIT remember credential temporaly</a></div></li>
    </ul>
  </div>
</div>
<!-- TOC END -->

<h1 class="sectionedit1" id="virtualbox_shared_folders_path">VirtualBox shared folders path</h1>
<div class="level1">

<p>
<strong>In VBox settings configuration:</strong><br/>

Folder path: C:\VirtualBoxSharedFolder<br/>

Folder name: shared<br/>

</p>

<p>
<a href="https://forums.virtualbox.org/viewtopic.php?f=3&amp;t=15868" class="urlextern" title="https://forums.virtualbox.org/viewtopic.php?f=3&amp;t=15868"  rel="nofollow">https://forums.virtualbox.org/viewtopic.php?f=3&amp;t=15868</a><br/>

</p>

<p>
In /etc/rc.local
</p>
<pre class="code">sudo gedit /etc/rc.local
sudo mount -t vboxsf -o rw,uid=1000,gid=1000 shared /home/alfredo/projects</pre>

</div>

<h1 class="sectionedit2" id="increase_hdd_size_in_virtualbox_machine">Increase HDD size in VirtualBox machine</h1>
<div class="level1">

<p>
1. Clone the machine
</p>

<p>
2. Inside vm folder, eg UbuntuDev1, change hd size to 12GB:
</p>
<pre class="code">C:\VirtualBox VM\UbuntuDev2&gt;&quot;c:\Program Files\Oracle\VirtualBox\vboxmanage.exe&quot; modifyhd &quot;UbuntuDev2-disk1.vdi&quot; --resize 12288</pre>

<p>
3. Start the machine
</p>

<p>
4. Extended and swap partitions must be eliminated to make free space be continuous to primary partition. Swap must be “Swapoff”
</p>

<p>
5. Increase partition size with “GParted” app. Left 1300 Bytes free for swapping
</p>

<p>
6. Create extended and swap partitions.
</p>

<p>
7. Restart.
</p>

</div>

<h1 class="sectionedit3" id="how_to_size_monitor_to_maximum_resolution">How to size monitor to maximum resolution</h1>
<div class="level1">
<ol>
<li class="level1"><div class="li"> Insert VBoxGuestAdditions Disk</div>
</li>
<li class="level1"><div class="li"> Autoruns </div>
</li>
<li class="level1"><div class="li"> Restart</div>
</li>
<li class="level1"><div class="li"> Settings: Set display resolution to max</div>
</li>
<li class="level1"><div class="li"> Host key + F</div>
</li>
</ol>

</div>

<h1 class="sectionedit4" id="how_to_enable_root_login">How to enable root login?</h1>
<div class="level1">

<p>
<a href="http://askubuntu.com/questions/44418/how-to-enable-root-login" class="urlextern" title="http://askubuntu.com/questions/44418/how-to-enable-root-login"  rel="nofollow">http://askubuntu.com/questions/44418/how-to-enable-root-login</a><br/>

</p>
<pre class="code">sudo passwd root</pre>

<p>
you will prompted for a new Unix password. Write it twice(second for confirmation).
</p>

<p>
Then execute
</p>
<pre class="code">sudo passwd -u root </pre>

<p>
Reverting back:<br/>

</p>
<pre class="code">sudo passwd -l root</pre>

</div>

<h1 class="sectionedit5" id="javascript_runtime">Javascript runtime</h1>
<div class="level1">

<p>
<a href="https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager#debian-and-ubuntu-based-linux-distributions" class="urlextern" title="https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager#debian-and-ubuntu-based-linux-distributions"  rel="nofollow">https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager#debian-and-ubuntu-based-linux-distributions</a>
Setup with Debian (as root):
</p>

<p>
<code>apt-get install curl</code><br/>

<code>curl -sL <a href="https://deb.nodesource.com/setup" class="urlextern" title="https://deb.nodesource.com/setup"  rel="nofollow">https://deb.nodesource.com/setup</a> | bash -</code><br/>

</p>

<p>
Then install with Debian (as root):<br/>

</p>

<p>
<code>apt-get install -y nodejs</code><br/>

</p>

<p>
<code>node -v</code>
</p>

</div>

<h2 class="sectionedit6" id="bowerfrontend_package_manager">Bower: frontend package manager</h2>
<div class="level2">

<p>
<code>npm install bower</code><br/>

</p>

</div>

<h1 class="sectionedit7" id="git_remember_credential_temporaly">GIT remember credential temporaly</h1>
<div class="level1">

<p>
Remember during 1 hour<br/>

<code>$ git config credential.helper &#039;cache –timeout=3600</code>&#039;
</p>

</div>