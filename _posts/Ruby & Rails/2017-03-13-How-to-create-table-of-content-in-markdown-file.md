---
layout: post
title: "How to create table of content in markdown file"
description: ""
category: [ruby, markdown]
tags: []
---
{% include JB/setup %}


    #create_toc.rb
    unless ARGV.empty?
      File.open(ARGV.first, 'r') do |f|
        f.each_line do |line|
          forbidden_words = ['Table of contents', 'define', 'pragma']
          next if !line.start_with?("#") || forbidden_words.any? { |w| line =~ /#{w}/ }
          title = line.gsub("#", "").strip
          href = title.downcase.gsub(" ", "-").gsub("--", "-").gsub(/'|\(|\)|\/|,|\./,"").gsub('á','a').gsub('é','e').gsub('í','i').gsub('ó','o').gsub('ú','u').gsub('Í','i')
          puts "  " * (line.count("#")-1) + "* [#{title}](\##{href})"
        end
      end
    else
      puts "Usage: ruby create_toc <md file>"
    end

Ejecutar

    ruby create_toc.rb path/to/README.md

para imprimir en pantalla el nuevo índice.
