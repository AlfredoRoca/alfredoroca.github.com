---
layout: post
title: "How to render html from controller action responding to pdf format"
description: ""
category: [rails]
tags: [pdf]
---
{% include JB/setup %}

      format.pdf do
        pdf = @emergency.generate_pdf_for_fax_and_email # generate pdf and save it into target folder ...
        # send_file pdf, type: 'application/pdf' # ... and download it
        response.content_type = Mime[:html]
        render 'inform_report_generated.html.erb'
      end
