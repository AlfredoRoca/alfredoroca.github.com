---
layout: post
title: "Cluster array - group adjacent values"
description: ""
category: [clustering]
tags: [array]
---
{% include JB/setup %}


<http://apidock.com/rails/Enumerable/group_by#508-Array-clustering>

Sometimes you don’t want to mangle sequence of an array and just want to group adjacent values. Here’s a nice method to do so (drop it in your initializers directory or something):

    module Enumerable
      # clumps adjacent elements together
      # >> [2,2,2,3,3,4,2,2,1].cluster{|x| x}
      # => [[2, 2, 2], [3, 3], [4], [2, 2], [1]]
      def cluster
        cluster = []
        each do |element|
          if cluster.last && yield(cluster.last.last) == yield(element)
            cluster.last << element
          else
            cluster << [element]
          end
        end
        cluster
      end
    end

Similarly you can do the clustering on more complex items. For instance you want to cluster Documents on creation date and their type:

    Document.all.cluster{|document| [document.created_on, document.type]}
