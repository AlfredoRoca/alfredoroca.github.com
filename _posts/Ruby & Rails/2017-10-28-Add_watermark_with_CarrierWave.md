---
layout: post
title: "Add watermark with CarrierWave"
description: ""
category: [ruby]
tags: [watermark, image]
---
{% include JB/setup %}

    process :watermark

    def watermark
    second_image = MiniMagick::Image.open("https://s3.amazonaws.com/....logo.png")
    manipulate! do |img|
      result = img.composite(second_image) do |c|
        c.compose "Over"    # OverCompositeOp
        c.gravity "Southeast" # copy second_image onto first_image from (20, 20)
      end
      result
      end
     end

or

    # Process files as they are uploaded:
    process :resize_to_fill => [850, 315]
    process :convert => 'png'
    process :watermark

    def watermark
      manipulate! do |img|
        logo = Magick::Image.read("#{Rails.root}/app/assets/images/watermark.png").first
        img = img.composite(logo, Magick::NorthWestGravity, 15, 0, Magick::OverCompositeOp)
      end
    end

