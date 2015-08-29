---
layout: post
title: ""
description: "Preventing data loss when leaving page with onbeforeunload event"
category: [js]
tags: [onbeforeunload]
---
{% include JB/setup %}

Source: <http://www.4guysfromrolla.com/webtech/100604-1.shtml>

    <script language="JavaScript">
      var ids = new Array('name', 'gender', 'sendEmail', 'radVanilla', 
                                        'radChocolate', 'radStrawberry');
      var values = new Array('', '', '', '', '', '');
      
      function populateArrays()
      {
        // assign the default values to the items in the values array
        for (var i = 0; i < ids.length; i++)
        {
          var elem = document.getElementById(ids[i]);
          if (elem)
            if (elem.type == 'checkbox' || elem.type == 'radio')
              values[i] = elem.checked;
            else
              values[i] = elem.value;
        }      
      }

      ...
    </script>

    ...

    <form ...>
      <b>What is your name:</b> <input type="text" id="name" name="name" /><br />
      <b>What is your gender?</b>
      <select id="gender" name="gender">
        <option value="Male">Male</option>
        <option value="Female">Female</option>
      </select><br />
      
      <input type="checkbox" name="sendEmail" id="sendEmail" /> <b>Send me your newsletter!</b>
      <br />
      <b>What is your favorite type of ice cream?</b><br />
      <input type="radio" id="radVanilla" name="iceCream" checked="checked" /> Vanilla<br />
      <input type="radio" id="radChocolate" name="iceCream" /> Chocolate<br />
      <input type="radio" id="radStrawberry" name="iceCream" /> Strawberry<br />
      <p>
      <input type="Submit" value="Save" onclick="needToConfirm = false;" />
    </form>

    <script language="JavaScript">
      populateArrays();
    </script>



