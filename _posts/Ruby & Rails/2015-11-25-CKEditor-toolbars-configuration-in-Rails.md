---
layout: post
title: "CKEditor toolbars configuration in Rails"
description: ""
category: [rails, ckeditor]
tags: []
---
{% include JB/setup %}


    # /app/assets/javascripts/ckeditor/config.js

    //
    // CKEditor customized config file - gem 'ckeditor_rails'
    //
    CKEDITOR.editorConfig = function(config) {
      config.language = 'es';
      config.toolbar_shk = [
        { name: 'basicstyles',  items: ['Bold', 'Italic', 'Underline', 'Strike', 'Subscript', 'Superscript', '-', 'RemoveFormat'] },
        { name: 'colors',       items: ['TextColor', 'BGColor'] },
        { name: 'paragraph',    items: ['NumberedList', 'BulletedList', '-', 'Outdent', 'Indent', '-', 'JustifyLeft', 'JustifyCenter', 'JustifyRight', 'JustifyBlock'] },
        '/',
        { name: 'styles',       items: ['Styles', 'Format', 'Font', 'FontSize'] },
        { name: 'insert',       items: ['Table', 'HorizontalRule', 'Smiley', 'SpecialChar'] },
      ];
      config.toolbar = 'shk';
      return true;
    };

