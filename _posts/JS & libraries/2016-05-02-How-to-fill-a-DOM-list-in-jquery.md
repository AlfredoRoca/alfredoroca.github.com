---
layout: post
title: "How to fill a DOM list/dropdown list in jquery"
description: ""
category: [jquery]
tags: []
---
{% include JB/setup %}


#Fill a list

HTML

    <ul id="list"></ul>

JS

    var fillList = function(array_of_options) {
        $("#list").empty();
        $.each(array_of_options, function(index, value) {
          newli = $( "<li>" + value['some_field'] + "</li>" );
          $("#list").append(newli);
        });
    }



#Fill a dropdown list

HTML

    <select id="options">

JS

      var fillDropdown = function(array_of_options) {
          $("#options").empty();
          $.each(array_of_options, function(index, value) {
            $("#options").append('<option value="' + value['some_field'] + '">' + value['another_field'] + '</option>');
          });
      }


