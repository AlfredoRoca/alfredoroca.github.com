---
layout: post
title: "Good reasons to replace db/schema.rb with db/structure.sql"
description: ""
category: [rails]
tags: []
---
{% include JB/setup %}



Source: <http://rubyofftherails.blogspot.com.es/2016/02/good-reasons-to-replace-dbschemarb-with.html>

Everybody knows that after running a

    $ rake db:migrate

the file db/schema.rb is updated to the present state of the application database. You may even rebuild this database by running

    $ rake db:schema:load

But db/schema.rb has two problems.

1) It is "Rails dependent"

If you want to reproduce this very same database out of a Rails environment, you just have to the heavy work yourself, recreating the tables. Without Rails framework you just don't have a way to generate all tables just based in db/schema.rb.

2) db/schema.rb does NOT support functions

So, if you need to use a function like "now()", db/schema.rb won't help. You may see a bit more about this here.

The solution for the two problems is changing the way Rails stores the database description. You won't use db/schema.rb anymore, but just a good old SQL dump named db/structure.sql.

You may do this easily by adding

config.active_record.schema_format = :sql

to your config/application.rb file.

From now on, the output of your migrations will be a file named db/structure.sql, with a traditional SQL dump of the database.

The only problem with this is the fact that Heroku doesn't like migrations in this format. Heroku is always demanding, as we already know. But there is a solution here too. Instead of just the like above, add to your config/application.rb the following code:

    if Rails.env == "production"
      config.active_record.schema_format = :ruby
    else
      config.active_record.schema_format = :sql
    end


