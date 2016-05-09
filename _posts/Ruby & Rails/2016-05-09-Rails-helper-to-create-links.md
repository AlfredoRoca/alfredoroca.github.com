---
layout: post
title: "Rails helper to create links"
description: ""
category: [rails, ruby]
tags: [helper]
---
{% include JB/setup %}



    def action_buttons(user)
        case current_user.friendship_status(user) when "friends"
            yield(link_to "Cancel Friendship", friendship_path(current_user.friendship_relation(user)), method: :delete, class: "btn btn-primary btn-xs")
        when "pending"
            yield(link_to "Cancel Request", friendship_path(current_user.friendship_relation(user)), method: :delete, class: "btn btn-primary btn-xs")
        when "requested"
            yield(link_to "Accept", accept_friendship_path(current_user.friendship_relation(user)), method: :put, class: "btn btn-primary btn-xs")
            yield(link_to "Decline", friendship_path(current_user.friendship_relation(user)), method: :delete, class: "btn btn-default btn-xs")
        when "not_friends"
            yield(link_to "Add as Friend", friendships_path(user_id: user.id), method: :post, class: "btn btn-primary btn-xs")
        end
    end

In this way, the template just provides the operation to do to each link in a block. 
That block might just be `{ |link| link }` if all you want is concatenation, but you could also have it wrap in tags or whatever. 
I'd still recommend factoring out the link_to so that it's less repetitive.





