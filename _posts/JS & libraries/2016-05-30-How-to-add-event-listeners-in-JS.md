---
layout: post
title: "How to add event listeners in JS"
description: ""
category: [js]
tags: [event listeners]
---
{% include JB/setup %}

Source: <https://www.developphp.com/video/JavaScript/Best-HTML-Event-Handling-addEventListener-Tutorial>

    <script>
    function addListeners(){
        if(window.addEventListener) {
            document.getElementById('mybtn').addEventListener("click",btn1func,false);
            document.getElementById('mybtn2').addEventListener("mouseover",btn2func,false);
        } else if (window.attachEvent){ // Added For Inetenet Explorer versions previous to IE9
            document.getElementById('mybtn').attachEvent("onclick", btn1func);
            document.getElementById('mybtn2').attachEvent("onmouseover",btn2func);
        }
        // Write your functions here
        function btn1func(){
            alert(this.id+" : mouse-click makes script run");
        }
        function btn2func(){
            alert(this.id+" : mouse-over makes script run");
        }
    }
    window.onload = addListeners; 
    </script> 

