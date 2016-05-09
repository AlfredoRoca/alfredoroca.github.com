---
layout: post
title: "Centering vertically with CSS"
description: ""
category: [html, css]
tags: []
---
{% include JB/setup %}

Source: <vanseodesign.com/blog/demo/vertical-centering/line-height.php>

More at: <http://vanseodesign.com/css/vertical-centering/>

# Centering vertically one line of text

HTML

    <div id="parent">
        <div id="child">Text here</div>
    </div>

CSS

    #child {
        line-height: 200px;
    }


The above works in all browsers, however it will *only work for a single line of text*. If your text could wrap to a 2nd line you need to use a different method. The value of 200px above is arbitrary. You can use any value you want as long as its *larger than the font-size* that’s been set.

Added: As Jeff pointed out in the comments below, there’s one small got’cha with this method in that you have to be careful when using the shortcut for the font property. This method relies on you setting the line-height as a value greater than the font-size. When you use the font shortcut any property you don’t specifically set gets set to its default value. With line-height that default is 1. If you use the font shortcut, just make sure to explicitly set the line-height inside.


# Centering vertically an image

HTML

    <div id="parent">
        <img src="image.png" alt="" />
    </div>

CSS

    #child {
        line-height: 200px;
    }

    #parent img {
        vertical-align: middle;
    }