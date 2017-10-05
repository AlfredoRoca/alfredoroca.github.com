---
layout: post
title: "How to include helpers in views directly"
description: ""
category: [rails]
tags: [views, helpers]
---
{% include JB/setup %}

### Use: add functionality for formatting purposes in Mailboxer emails.

Mailboxer gem exposes views but it can not use Rails mailer layouts (or I don't know how to do it). This is my solution to customize mailboxer mails.

    # views/mailboxer/message_mailer/new_message_email.html.erb

    <% self.class.send :include, EmailHelper %>
    
    <!DOCTYPE html>
    <html>
      <head>
        <meta content="text/html; charset=UTF-8" http-equiv="Content-Type" />
      </head>
      <body>
        <% background = ActionController::Base.helpers.image_url('madera.png') %>

        <%= email_tag(:div) do %>
          <div style="background: url(<%= background %>);">

            <%= email_tag :header do %>
              <%= image_tag image_url('logo_sharing_kitchen-cabecera-blanco-sombreado.png'), width: '300px', alt: "Sharing-Kitchen " %>
            <% end -%>

            <div style="padding: 0 2em;">

              <p><%= t(:You_have_received_a_new_message) %>:</p>
              <blockquote>
                <p>
                  <%= raw @message.body %>
                </p>
              </blockquote>
              <p></p>
              <p><%= t(:Visit) %> <%= link_to root_url, root_url %> <%= t(:and_go_to_your_inbox_for_more_info) %></p>

              <p><%= t(:Thanks_for_trusting) %></p>
              <p><%= t(:Regards) %></p>
              <p><%= t(:Sharing_Kitchen_team) %></p>
            </div>

            <%= email_tag :footer do %>
              <p style="padding: 0 2em 2em 2em;"><em>© Sharing-Kitchen.com - <%= Time.current.year %></em> <%= " - #{Rails.env.upcase}" unless Rails.env.production? %></p>
            <% end %>

          </div>
        <% end -%>

      </body>
    </html>


The helper

    # helpers/email_helper.rb

    module EmailHelper

      STYLES = {
        h1: 'margin-bottom: 20px; margin-top: 10px; font-size: 32px;',
        h2: 'margin-bottom: 10px; margin-top: 15px; font-size: 18px;',
        h3: 'margin-bottom: 10px; margin-top: 15px; font-size: 14px;',
        a: 'text-decoration: none; color: #32aeee;',
        p: 'margin-bottom: 10px; line-height: 20px;',
        img: 'text-align:center; margin-block-end: 20px;', # with image - margin is not applied ¿?
        header: 'text-align: center',
        footer: 'margin-bottom: 10px; margin-top: 15px; font-size: 12px; border-top: 2px solid black;',
        div: "max-width: 600px; text-align: justify; font-family: Montserrat, Tahoma, Helvetica, sans-serif;",
      }

      def email_tag(type, options = {}, &content)
        options[:style] ||= STYLES[type]
        options[:target] = '_blank' if type == :a
        type = :div if type == :img
        content_tag type, options, &content
      end

    end

