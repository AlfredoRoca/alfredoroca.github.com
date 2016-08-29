---
layout: post
title: "Benchmarking in ruby"
description: ""
category: [benchmarking]
tags: []
---
{% include JB/setup %}


## Example: finding longest word in an array

    require 'benchmark'

    def m1
      %w{perro leon armario cazador escopeta arco}.inject{|memo, word| memo.length >  word.length ? memo : word}
    end

    def m2
      %w{perro leon armario cazador escopeta arco}.max{|a,b| a.length <=> b.length}
    end


    def m3
      %w{perro leon armario cazador escopeta arco}.max_by{|word| word.length}
    end

    n = 1000000
    Benchmark.bm(7) do |x|
      x.report("inject:") { n.times {m1} }
      x.report("max:") { n.times {m2} }
      x.report("max_by:") { n.times {m3} }
    end


    Results:
                  user     system      total        real
    inject:   2.170000   0.000000   2.170000 (  2.356248)
    max:      2.210000   0.020000   2.230000 (  2.429657)
    max_by:   2.100000   0.030000   2.130000 (  2.316363)


## Benchmarking Activerecord commands

    require 'benchmark'
    n=1000
    Benchmark.bm(7) do |x|
      x.report("map: ") {n.times { User.all.includes(:contracted_plans).map{|u| [u] if (u.current_contracted_plan.nil? || u.current_contracted_plan.is_cancelled?) }.compact.flatten }}
      x.report("ids: ") {n.times { User.all.where.not(id: ContractedPlan.all.pluck(:user_id)) }}
    end




