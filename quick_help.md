---
layout: page
title: "Quick help"
group: navigation
---
{% include JB/setup %}

# New post creation
    rake post title="new post title" [tags=[tag1,tag2]] [category=[category1, category2]]

# Generate Table of contents from the markdown file

`create_toc.rb`

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

To print table of contents to screen execute

    ruby create_toc.rb path/to/README.md


# Markdown sintaxis
[http://daringfireball.net/projects/markdown/syntax](http://daringfireball.net/projects/markdown/syntax){:target="_blank"}

[http://greg.schueler.us/doc/markdown.txt](http://greg.schueler.us/doc/markdown.txt){:target="_blank"}

[http://blog.ghost.org/markdown/](http://support.ghost.org/markdown-guide/){:target="_blank"}

<http://stackoverflow.com/editing-help>

<https://guides.github.com/features/mastering-markdown/>


# Liquid

[https://github.com/Shopify/liquid/wiki/Liquid-for-Designers](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers){:target="_blank"}

