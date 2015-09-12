---
layout: post
title: ""
description: ""
category: [capistrano, airbrush]
tags: []
---
{% include JB/setup %}

<https://github.com/mattbrictson/airbrussh>

gemfile

    # Airbrussh is a replacement log formatter for SSHKit that makes your Capistrano output much easier on the eyes
    gem "airbrussh", :require => false

capfile

    require "airbrussh/capistrano"

deploy.rb

    # Remove this
    set :format, :pretty

    Airbrussh.configure do |config|
      # Capistrano's default, un-airbrusshed output is saved to a file to
      # facilitate debugging.
      #
      # To disable this entirely:
      # config.log_file = nil
      #
      # Default:
      config.log_file = "log/capistrano.log"

      # Airbrussh patches Rake so it can access the name of the currently executing
      # task. Set this to false if monkey patching is causing issues.
      #
      # Default:
      config.monkey_patch_rake = true

      # Ansi colors will be used in the output automatically based on whether the
      # output is a TTY, or if the SSHKIT_COLOR environment variable is set.
      #
      # To disable color always:
      # config.color = false
      #
      # Default:
      config.color = :auto

      # Output is automatically truncated to the width of the terminal window, if
      # possible. If the width of the terminal can't be determined, no truncation
      # is performed.
      #
      # To truncate to a fixed width:
      # config.truncate = 80
      #
      # Or to disable truncation entirely:
      # config.truncate = false
      #
      # Default:
      config.truncate = :auto

      # If a log_file is configured, airbrussh will output a message at startup
      # displaying the log_file location.
      #
      # To always disable this message:
      # config.banner = false
      #
      # To display an alternative message:
      # config.banner = "Hello, world!"
      #
      # Default:
      config.banner = :auto

      # You can control whether airbrussh shows the output of SSH commands. For
      # brevity, the output is hidden by default.
      #
      # Display stdout of SSH commands. Stderr is not displayed.
      config.command_output = :stdout
      #
      # Display stderr of SSH commands. Stdout is not displayed.
      # config.command_output = :stderr
      #
      # Display all SSH command output.
      # config.command_output = [:stdout, :stderr]
      # or
      # config.command_output = true
      #
      # Default (all output suppressed):
      # config.command_output = false
    end


For brevity, airbrussh mutes all output (stdout and stderr) of commands by default. 
To show all output, add this to your ```deploy.rb``` (see also the other configuration options later in this README):

    Airbrussh.configure do |config|
      config.command_output = true
    end

