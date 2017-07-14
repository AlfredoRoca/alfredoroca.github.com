---
layout: post
title: "Stub vs query"
description: ""
category: [test]
tags: [stub]
---
{% include JB/setup %}

Old sintaxis

**Hiting the database**

    context "given an article with an average score of 4" do
      setup do
        @article = Factory(:article)
        3.times { Factory(:vote, :article => @article, :score => 4) }
      end

      should "display the score on GET to show" do
        get :show, :id => @article.to_param
        assert_select '.score', '4'
      end
    end


**Stubing**

    context "given an article with an average score of 4" do
      setup do
        @article = Factory(:article)
        @article.stubs(:score => 4)
        Article.stubs(:find).with(@article.id).returns(@article)
      end

      should "display the score on GET to show" do
        get :show, :id => @article.to_param
        assert_select '.score', '4'
      end
    end