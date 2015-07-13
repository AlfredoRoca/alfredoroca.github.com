---
layout: post
title: "Image upload"
description: ""
category: Image Upload
tags: [Image, upload]
---
{% include JB/setup %}

<!-- TOC START -->
<div id="dw__toc">
<h3 class="toggle">Table of Contents</h3>
<div>

<ul class="toc">
<li class="level1"><div class="li"><a href="#web_app_with_image_uploader">Web app with image uploader</a></div>
<ul class="toc">
<li class="level2"><div class="li"><a href="#delegates">Delegates</a></div></li>
<li class="level2"><div class="li"><a href="#imagemagick">ImageMagick</a></div></li>
</ul>
</li>
<li class="level1"><div class="li"><a href="#configuration">Configuration</a></div></li>
<li class="level1"><div class="li"><a href="#recreate_versions">Recreate versions</a></div></li>
<li class="level1"><div class="li"><a href="#nginx_error_-_413_request_entity_too_large">Nginx Error - 413 Request Entity Too Large</a></div></li>
</ul>
</div>
</div>
<!-- TOC END -->

<h1 class="sectionedit1" id="web_app_with_image_uploader">Web app with image uploader</h1>
<div class="level1">

<p>
<a href="https://github.com/carrierwaveuploader/carrierwave" class="urlextern" title="https://github.com/carrierwaveuploader/carrierwave"  rel="nofollow">https://github.com/carrierwaveuploader/carrierwave</a><br/>

<a href="https://github.com/minimagick/minimagick" class="urlextern" title="https://github.com/minimagick/minimagick"  rel="nofollow">https://github.com/minimagick/minimagick</a><br/>

<a href="http://www.imagemagick.org/script/install-source.php" class="urlextern" title="http://www.imagemagick.org/script/install-source.php"  rel="nofollow">http://www.imagemagick.org/script/install-source.php</a><br/>

<a href="http://www.imagemagick.org/discourse-server/viewtopic.php?t=22086" class="urlextern" title="http://www.imagemagick.org/discourse-server/viewtopic.php?t=22086"  rel="nofollow">http://www.imagemagick.org/discourse-server/viewtopic.php?t=22086</a><br/>

<a href="http://www.imagemagick.org/download/delegates/" class="urlextern" title="http://www.imagemagick.org/download/delegates/"  rel="nofollow">http://www.imagemagick.org/download/delegates/</a><br/>

</p>

</div>

<h2 class="sectionedit2" id="delegates">Delegates</h2>
<div class="level2">

<p>
Download from delegates, decompress and install codecs libs (maybe there are new versions)<br/>

</p>
<pre class="code">tar -xvf jpegsrc.v9a.tar.gz 
tar -xvf libpng-1.6.16.tar.gz
cd jpeg-9a/
./configure
make
make test
sudo make install

cd ../libpng-1.6.16/
./configure
make
make test
sudo make install</pre>

</div>

<h2 class="sectionedit3" id="imagemagick">ImageMagick</h2>
<div class="level2">

<p>
Download the latest version, decompress and install ImageMagick <a href="http://mirror.checkdomain.de/imagemagick/" class="urlextern" title="http://mirror.checkdomain.de/imagemagick/"  rel="nofollow">http://mirror.checkdomain.de/imagemagick/</a>
</p>
<pre class="code">tar xvfz ImageMagick-6.9.1-2.tar.gz
cd ImageMagick-6.9.1-2
./configure &#039;--with-png=yes&#039; &#039;--with-jpeg=yes&#039; &#039;--with-jp2=yes&#039; &#039;--with-freetype=yes&#039;
make
sudo make install
sudo ldconfig /usr/local/lib
/usr/local/bin/convert logo: logo.gif
make check
identify -list configure</pre>

</div>

<h1 class="sectionedit4" id="configuration">Configuration</h1>
<div class="level1">

<p>
Follow the gems documentation.
</p>
<pre class="code"># /config/minimagick.rb
MiniMagick.configure do |config|
  config.whiny = false
end</pre>

</div>

<h1 class="sectionedit5" id="recreate_versions">Recreate versions</h1>
<div class="level1">
<pre class="code">Product.all.each do |product|
  product.photos.each do |photo|
    photo.recreate_versions!
  end
end</pre>

</div>

<h1 class="sectionedit6" id="nginx_error_-_413_request_entity_too_large">Nginx Error - 413 Request Entity Too Large</h1>
<div class="level1">
<pre class="code"># /etc/nginx/nginx.conf
server {
      client_max_body_size 20M;
      listen       80;</pre>

</div>