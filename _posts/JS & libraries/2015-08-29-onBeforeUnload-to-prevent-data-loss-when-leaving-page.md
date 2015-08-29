---
layout: post
title: "Preventing data loss when leaving page with onbeforeunload event"
description: ""
category: [js]
tags: [onbeforeunload]
---
{% include JB/setup %}

    window.onbeforeunload = function () {return false;}

    //
    // demo
    //
    function confirmExit() {
      if (needToConfirm) {
      // check to see if any changes to the data entry fields have been made
      // no changes - return nothing
        if ($(".invisible").length < 4) {
          return true;
        }
      }
    }

Source: <http://www.4guysfromrolla.com/webtech/100604-1.shtml>

    <script language="JavaScript">
      var ids = new Array('name', 'gender', 'sendEmail', 'radVanilla', 'radChocolate', 'radStrawberry');
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



      var needToConfirm = true;
      
      window.onbeforeunload = confirmExit;
      function confirmExit()
      {
        if (needToConfirm)
        {
          // check to see if any changes to the data entry fields have been made
          for (var i = 0; i < values.length; i++)
          {
            var elem = document.getElementById(ids[i]);
            if (elem)
              if ((elem.type == 'checkbox' || elem.type == 'radio')
                      && values[i] != elem.checked)
                return "You have attempted to leave this page.  If you have made any changes to the fields without clicking the Save button, your changes will be lost.  Are you sure you want to exit this page?";
              else if (!(elem.type == 'checkbox' || elem.type == 'radio') &&
                      elem.value != values[i])
                return "You have attempted to leave this page.  If you have made any changes to the fields without clicking the Save button, your changes will be lost.  Are you sure you want to exit this page?";
          }

          // no changes - return nothing      
        }
      }
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
