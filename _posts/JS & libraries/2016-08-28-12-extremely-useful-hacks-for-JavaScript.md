---
layout: post
title: "12 extremely useful hacks for JavaScript"
description: ""
category: [js, hacks]
tags: []
---
{% include JB/setup %}



<https://blog.jscrambler.com/12-extremely-useful-hacks-for-javascript/?utm_source=javascriptweekly&utm_medium=email>

1) Converting to boolean using !! operator

    function Account(cash) {
        this.cash = cash;
        this.hasMoney = !!cash;
    }

2) Converting to number using + operator

    function toNumber(strNumber) {
        return +strNumber;
    }
    console.log(toNumber("1234")); // 1234
    console.log(toNumber("ACB")); // NaN

3) Short-circuits conditionals

    user && user.login();

4) Default values using || operator

    this.name = name || "Oliver Queen";

5) Caching the array.length in the loop

    for(var i = 0, length = array.length; i < length; i++) {
        console.log(array[i]);
    }

6) Detecting properties in an object

    if ('querySelector' in document) {
        document.querySelector("#id");
    } else {
        document.getElementById("id");
    }

7) Getting the last item in the array

    var array = [1,2,3,4,5,6];
    console.log(array.slice(-1)); // [6]
    console.log(array.slice(-2)); // [5,6]
    console.log(array.slice(-3)); // [4,5,6]

8) Array truncation

    var array = [1,2,3,4,5,6];
    console.log(array.length); // 6
    array.length = 3;
    console.log(array.length); // 3
    console.log(array); // [1,2,3]

9) Replace all

    /g 

    string.replace(/hn/g, "ana"))

10) Merging arrays

    Array.concat()

11) Converting NodeList to Arrays

    [].slice.call(elements) / Array.from(elements)

    var elements = document.querySelectorAll("p"); // NodeList
    var arrayElements = [].slice.call(elements); // Now the NodeList is an array
    var arrayElements = Array.from(elements); // This is another way of converting NodeList to Array

12) Shuffling array’s elements

    var list = [1,2,3];
    console.log(list.sort(function() { Math.random() - 0.5 })); // [2,1,3]

