---
layout: post
title: "Rails performance considerations"
description: ""
category: [rails]
tags: [performance]
---
{% include JB/setup %}



Rails 3.1 introduced the concept of the asset pipeline. Unfortunately, this causes some significant performance issues when running Spree in development mode. The good news is you can improve performance significantly by using a special precompile task.

    $ bundle exec rake assets:precompile:nondigest

Using the precompile rake task in development will prevent any changes to asset files from being automatically included in when you reload the page. You must re-run the precompile task for changes to become available.

Rails also provides the following rake task that will delete the entire public/assetsdirectory, this can be helpful to clear out development assets before committing.

    $ bundle exec rake assets:clean

It might also be worthwhile to include the `public/assets` directory in your `.gitignore` file.