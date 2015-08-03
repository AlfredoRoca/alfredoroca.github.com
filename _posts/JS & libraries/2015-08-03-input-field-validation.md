---
layout: post
title: "Input field validation in JS"
description: ""
category: [JS]
tags: [input form validation]
---
{% include JB/setup %}

JS

    iban = "string";  
    re = /^[a-zA-Z]{2}\d{2}\s*([0-9]{4}\s*){5}$/;  
    valid = iban.match(re) != null;

In the model

    def valid_iban?    
      re = /^[a-zA-Z]{2}\d{2}\s*([0-9]{4}\s*){5}$/;    
      valid = re.match(iban) != nil;  
    end

Example

    #
    # validate-iban.js
    #
    var validateIban;
    var bindIbanValidation;

    bindIbanValidation = function () {  
      $('#user_bank_account_iban').on('keyup', validateIban);  validateIban();
    };
    validateIban = function () {  
      iban = $('#user_bank_account_iban').val();
      re = /^[a-zA-Z]{2}\d{2}\s*([0-9]{4}\s*){5}$/;
      valid = iban.match(re) != null;
      if (valid) {    
          $('#valid-iban').removeClass('invisible');
          $('#invalid-iban').addClass('invisible');
          $('#user_bank_account_iban').addClass('valid-iban');
          $('#user_bank_account_iban').removeClass('invalid-iban');
      } else {
          $('#valid-iban').addClass('invisible');
          $('#invalid-iban').removeClass('invisible');
          $('#user_bank_account_iban').removeClass('valid-iban');
          $('#user_bank_account_iban').addClass('invalid-iban');
      }}

    // $(document).ready(bindIbanValidation);
    $(document).on('page:load', bindIbanValidation);


    #
    # bank_account.html.erb
    #
    <% content_for :js do %>  
      <%= javascript_include_tag 'validate-iban.js', 'data-turbolinks-track' => true %>
    <% end -%>
    <h3><%= label_tag t(:Bank_account_information) %></h3>
    <div class="form-group">  
        <div class="col-sm-4 control-label">
          <%= @f.label(:iban, t(:iban) << " (*)") %>
        </div>
        <div class="col-sm-7 with-validation-marks">
          <%= @f.text_field :bank_account_iban, class: "form-control" %>
          <label id="valid-iban" class="validity-symbol valid-iban"><%= "\u2713" %></label>
          <label id="invalid-iban" class="validity-symbol invalid-iban"><%= "\u2717" %></label> <br>
          <label class="space-hint"><%= t(:hint_for_bank_account_validation) %></label>
        </div>
    </div>
    <div class="form-group">
      <div class="col-sm-4 control-label">
        <%= @f.label t :owner %>
      </div>  
      <div class="col-sm-8">
        <%= @f.text_field :bank_account_owner, class: "form-control", placeholder: @user.fullname %>    
        <label class="space-hint"><%= t(:hint_for_bank_account_owner) %></label>
      </div>
    </div>
    <div class="spacer"></div>
    <div class="required"><%= t(:required_fields) %></div>

    <script>bindIbanValidation();
    </script>

    #
    # profile.scss
    #

    .with-validation-marks {  
      input {    
        width: 25em;
        display: inline;
      }  
      .validity-symbol {
        vertical-align: top;
        font-size: 2em;
        height: 1em;
      }
      .valid-iban {
        color: green;
        input {
          border: 2px solid green;
        }
      }  
      .invalid-iban {
        color: red;
        input {
          border: 2px solid red;
        }  
      }
    }


