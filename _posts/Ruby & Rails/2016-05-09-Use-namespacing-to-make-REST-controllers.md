---
layout: post
title: "Use namespacing to make REST controllers"
description: ""
category: [ruby, rails, rest]
tags: []
---
{% include JB/setup %}



Convert

    class InboxesController < ApplicationController
      def index
      end

      def pendings
      end
    end


into

    class InboxesController < ApplicationController
      def index
      end
    end

    class Inboxes::PendingsController < ApplicationController
      def index
      end
    end
