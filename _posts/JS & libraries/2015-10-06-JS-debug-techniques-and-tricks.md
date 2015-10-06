---
layout: post
title: "JS debugging techniques and tricks"
description: ""
category: [js, debug]
tags: []
---
{% include JB/setup %}

Source: <https://raygun.io/blog/2015/06/useful-javascript-debugging-tips-you-didnt-know/?utm_source=JSNewsletter25&utm_medium=SponsoredLink&utm_campaign=CooperPressSept15>

#Quick find your DOM elements.
Mark elements and quickly find them in console with $0, $1, .. up to $4

#Display object as tables
write ```console.table(variable)``` in JS code to see it like table in JS console

#Get the stack trace for a function
in JS console write ```trace var```

#Quick find a function to debug
in console write ```debug(function-name)```

#Black box scripts that are NOT relevant
source: <https://raygun.io/blog/2015/05/javascript-debugging-with-black-box/>

#Find the important things in complex debugging

    console.todo = function( msg){
        console.log( '%c %s %s %s ', 'color: yellow; background-color: black;', '--', msg, '--');
    }
    console.important = function( msg){
        console.log( '%c%s %s %s', 'color: brown; font-weight: bold; text-decoration: underline;', '--', msg, '--');
    }
    console.todo("This is something that's need to be fixed");
    console.important('This is an important message');
