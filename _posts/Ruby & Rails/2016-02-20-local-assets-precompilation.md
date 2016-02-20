---
layout: post
title: "What is needed to precompile assets locally?"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}


Source: <https://www.reinteractive.net/posts/116-12-tips-for-the-rails-asset-pipeline>

To precompile locally, you need to do the following:

1. Setup a dummy production database on your local machine
1. Create a production entry in database.yml
1. Add in any other dummy settings to load a production environment
1. Run RAILS_ENV=production rake assets:clean assets:precompile
1. Wait
1. Wait some more
1. Commit the results in the public/assets folder


