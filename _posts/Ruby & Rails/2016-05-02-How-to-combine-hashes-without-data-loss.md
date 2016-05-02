---
layout: post
title: "How to combine hashes without data loss"
description: ""
category: []
tags: []
---
{% include JB/setup %}



    hash1={"a"=>1,"b"=>2,"c"=>3}
    => {"a"=>1, "b"=>2, "c"=>3}

    hash2={"c"=>4, "d"=>5,"a"=>3}
    => {"a"=>3, "c"=>4, "d"=>5}

    hash1.merge(hash2)
    => {"a"=>3, "b"=>2, "c"=>4, "d"=>5} #"a"=>1 & "c"=>3 items in hash1 were lost

    hash1.merge(hash2){|key, oldval, newval| [*oldval].to_a + [*newval].to_a }
    => {"a"=>[1, 3], "b"=>2, "c"=>[3, 4], "d"=>5}


