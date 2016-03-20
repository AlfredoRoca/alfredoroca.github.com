---
layout: post
title: "Loops in Bash"
description: ""
category: [bash, loops, for, while, until]
tags: []
---
{% include JB/setup %}


# for

    for variable-name in list
    do
        execute one iteration for each item in the
                list until the list is finished
    done

Example

    sum=0
    for i in 1 2 3 4
    do
    sum=$(($sum+$i))
    done
    echo $sum


# while

    while condition is true
    do
        Commands for execution
        ----
    done

Example

    echo "enter number"
    read num
    fact=1
    i=1
    while [ $i -le $num ]
    do
            fact=$(($fact*$i))
            i=$(($i+1))
    done
    echo "Fact de $num is $fact"

# until

    until condition is false
    do
        Commands for execution
        ----
    done

Example

    echo "waiting..."
    mn=1
    mx=10
    until [ $mn -gt $mx ]
    do
            echo "$mn"
            mn=$(($mn+1))
    done
    echo "ready"
