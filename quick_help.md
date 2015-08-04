---
layout: page
title: "Quick help"
group: navigation
---
{% include JB/setup %}

# Generate Table of contents from the markdown file

    # create_toc.rb
    With next ruby code:
    unless ARGV.empty? 
      File.open(ARGV.first, 'r') do |f|
        f.each_line do |line|
          forbidden_words = ['Table of contents', 'define', 'pragma']
          next if !line.start_with?("#") || forbidden_words.any? { |w| line =~ /#{w}/ }
          title = line.gsub("#", "").strip
          href = title.gsub(" ", "-").downcase
          puts "  " * (line.count("#")-1) + "* [#{title}](\##{href})"
        end
      end
    else
      puts "Usage: ruby create_toc <md file>"
    end

# New post creation
    rake post title="new post title"

# Markdown sintaxis
[http://daringfireball.net/projects/markdown/syntax](http://daringfireball.net/projects/markdown/syntax){:target="_blank"}

[http://greg.schueler.us/doc/markdown.txt](http://greg.schueler.us/doc/markdown.txt){:target="_blank"}

[http://blog.ghost.org/markdown/](http://support.ghost.org/markdown-guide/){:target="_blank"}

#Liquid
[https://github.com/Shopify/liquid/wiki/Liquid-for-Designers](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers){:target="_blank"}