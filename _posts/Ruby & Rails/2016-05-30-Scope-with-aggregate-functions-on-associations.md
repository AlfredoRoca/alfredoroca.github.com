---
layout: post
title: "Scope with aggregate functions on associations"
description: ""
category: [rails]
tags: [activerecord]
---
{% include JB/setup %}

    Space has_many spacephotos

    scope :with_photos, -> { joins(:spacephotos).group("spaces.id").having("count(*) > 0") }

    Space.with_photos
    => SELECT "spaces".* FROM "spaces" INNER JOIN "spacephotos" ON "spacephotos"."space_id" = "spaces"."id" GROUP BY spaces.id HAVING count(*) > 0

    Space.with_photos.count
    => SELECT COUNT(*) AS count_all, spaces.id AS spaces_id FROM "spaces" INNER JOIN "spacephotos" ON "spacephotos"."space_id" = "spaces"."id" GROUP BY spaces.id HAVING count(*) > 0
