---
layout: post
title: "Google analytics in Rails"
description: ""
category: [google-analytics]
tags: []
---
{% include JB/setup %}

Because Rails apps can use turbolinks, Google's JS snippet must be tweaked:

    use the page:change event, and track pageviews, not events.
    - Comment 'pageview' line
    - add it to a JS file loaded in the asset pipeline

For example, in your <head>:

    <% if Rails.env.production? %>
      <script>
        (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
        (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
        m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
        })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

        ga('create', 'UA-XXXXXXXX-X', 'auto');
        //ga('send', 'pageview');
      </script>
    <% else %>
      <script>
        function ga () {
          var params = Array.prototype.slice.call(arguments, ga.length);
          console.log("GoogleAnalytics: " + params);
        };
      </script>
    <% end %>

And then in a js file you have loaded through the asset pipeline:

    // ga.js
    $(document).on('page:change', function() {
      ga('send', 'pageview', window.location.pathname);
    });


    // application.js
    //= require ga 

This will record a pageview for each page you load with or without Turbolinks. Note that the window.location.pathname is required, otherwise you can get the URL of the first page loaded for all the subsequent page loads. (This also gives you a nice place to edit the URL reported if you wanted to, say, strip out :id path segments from RESTful URLs.)

You can also then easily call:

    ga('send', "event", category, action, label, count);

To report Events for other interesting javascript events in your site.

Google's source: <https://developers.google.com/analytics/devguides/collection/analyticsjs/command-queue-reference#send>
Samples:

    // Sends a pageview hit.
    ga('send', 'pageview');

    // Sends an event hit for the tracker named "myTracker" with the
    // following category, action, and label, and sets the nonInteraction
    // field value to true.
    ga('send', 'event', 'link', 'click', 'http://example.com', {
      nonInteraction: true
    });
