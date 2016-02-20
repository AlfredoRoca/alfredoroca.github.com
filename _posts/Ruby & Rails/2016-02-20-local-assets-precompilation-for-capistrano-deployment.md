---
layout: post
title: "What is needed to precompile assets locally?"
description: ""
category: [rails, capistrano]
tags: []
---
{% include JB/setup %}

Asset pipeline: <http://guides.rubyonrails.org/asset_pipeline.html#in-production>

There are three caveats:

- You must not run the Capistrano deployment task that precompiles assets.
- You must ensure any necessary compressors or minifiers are available on your development system.
- You must change the following application configuration setting:

Capistrano:

<http://capistranorb.com/documentation/advanced-features/overriding-capistrano-tasks/#>

deploy.rb:

    # clear the previous precompile task
    Rake::Task["deploy:assets:precompile"].clear_actions

development.rb

    # this prefix prevents serving compiled assets in development
    config.assets.prefix = '/assets_dev'


.gitignore

    public/assets-dev


Nginx:

    location ~ ^/assets/ {
      expires 1y;
      add_header Cache-Control public;
     
      add_header ETag "";
      break;
    }


Source: <https://www.reinteractive.net/posts/116-12-tips-for-the-rails-asset-pipeline>

To precompile locally, you need to do the following:

1. Setup a dummy production database on your local machine
1. Create a production entry in database.yml
1. Add in any other dummy settings to load a production environment
1. Run RAILS_ENV=production rake assets:clean assets:precompile
1. Wait
1. Wait some more
1. Commit the results in the public/assets folder
1. Deploy this


