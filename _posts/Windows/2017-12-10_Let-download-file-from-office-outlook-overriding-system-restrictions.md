---
layout: post
title: "Let download files from links in Outlook mail messages overriding system restrictions"
description: ""
category: [windows]
tags: []
---
{% include JB/setup %}

Create a file LINKS.CMD with following content and execute as administrator

    REG ADD HKEY_CURRENT_USER\Software\Classes\.htm /ve /d htmlfile /F
    REG ADD HKEY_CURRENT_USER\Software\Classes\.html /ve /d htmlfile /F 
    REG ADD HKEY_CURRENT_USER\Software\Classes\.shtml /ve /d htmlfile /F 
    REG ADD HKEY_CURRENT_USER\Software\Classes\.xht /ve /d htmlfile /F 
    REG ADD HKEY_CURRENT_USER\Software\Classes\.xhtml /ve /d htmlfile /F
