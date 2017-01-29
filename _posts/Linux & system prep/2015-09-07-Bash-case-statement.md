---
layout: post
title: "Case statement in Bash"
description: ""
category: [bash]
tags: [case]
---
{% include JB/setup %}


    case expression in
      pattern1) execute commands;;
      pattern2) execute commands;;
      pattern3) execute commands;;
      pattern4) execute commands;;
      * ) execute else or nothing
    ;;

    esac

Example

    echo "Enter a letter"
    read letter
    case "$letter" in
      "a"|"A") echo "Yoou entered vowel a" ;;
      "b"|"B") echo "You entered a consonant b" ;;
      *) echo "you entered somthing else" ;;
    esac
