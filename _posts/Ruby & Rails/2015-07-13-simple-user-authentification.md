---
layout: post
title: "Simple user authentification"
description: ""
category: [rails] 
tags: [authentification]
---
{% include JB/setup %}


    # gemfile
    gem 'bcrypt', '~> 3.1.7'

`$ rails g model user name password_digest:text`

    # user.rb
    has_secure_password
    validates :name, :email, presence: true, length: { in: 2..255 }

`$ rails g controller sessions new`

    # sessions controller.rb
    class SessionsController < ApplicationController
    def new
    end
    def create
      user = User.find_by(name: params[:name])
      if user && user.authenticate(params[:password])
        session[:user_id] = user.id
        redirect_to root_url
      else
        render :new
      end
    end
    def destroy
      session[:user_id] = nil
      redirect_to root_url
    end
    end

.

    # sessions/new.html.erb
    <h1>Login</h1>
    <%= form_tag sessions_path do %>
    <%= label_tag :name %>
    <%= text_field_tag :name %>
    <%= label_tag :password %>
    <%= password_field_tag :password %>
    <%= submit_tag "Log in" %>
    <% end %>

`$ rails g controller welcome index`

    # welcome_controller.rb
    def index
    end

.

    # welcome/index.html.erb
    <h1>Welcome</h1>

.

    # application_controller.rb
    def current_user
      if session[:user_id]
        current_user = User.find(session[:user_id])
      end
    end
    helper_method :current_user

in the action controllers

    before_action :authenticate_user

    def authenticate_user
      redirect_to login_path unless current_user 
    end





-----------------------
<h1 class="sectionedit1" id="simple_user_authentication">Simple user authentication</h1>
<div class="level1">
<pre class="code"># gemfile
gem &#039;bcrypt&#039;, &#039;~&gt; 3.1.7&#039;</pre>
<pre class="code">$ rails g model user name password_digest:text</pre>
<pre class="code"># user.rb
has_secure_password
validates :name, :email, presence: true, length: { in: 2..255 }</pre>
<pre class="code">$ rails g controller sessions new</pre>
<pre class="code"># sessions controller.rb
class SessionsController &lt; ApplicationController
def new
end
def create
  user = User.find_by(name: params[:name])
  if user &amp;&amp; user.authenticate(params[:password])
    session[:user_id] = user.id
    redirect_to root_url
  else
    render :new
  end
end
def destroy
  session[:user_id] = nil
  redirect_to root_url
end
end</pre>
<pre class="code"># sessions/new.html.erb
&lt;h1&gt;Login&lt;/h1&gt;
&lt;%= form_tag sessions_path do %&gt;
&lt;%= label_tag :name %&gt;
&lt;%= text_field_tag :name %&gt;
&lt;%= label_tag :password %&gt;
&lt;%= password_field_tag :password %&gt;
&lt;%= submit_tag &quot;Log in&quot; %&gt;
&lt;% end %&gt;</pre>
<pre class="code">$ rails g controller welcome index</pre>
<pre class="code"># welcome_controller.rb
def index
end</pre>
<pre class="code"># welcome/index.html.erb
&lt;h1&gt;Welcome&lt;/h1&gt;</pre>
<pre class="code"># application_controller.rb
def current_user
  if session[:user_id]
    current_user = User.find(session[:user_id])
  end
end
helper_method :current_user</pre>
<pre class="code"># in the action controllers
before_action :authenticate_user

def authenticate_user
  redirect_to login_path unless current_user 
end</pre>

</div>