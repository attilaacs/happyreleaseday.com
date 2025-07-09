---
layout: post
title:  "Formatting sheet for text fields"
date:   2025-07-09 16:40:43 +1000
categories: swiftui
---

The original idea was to have text fields and color control below the video preview. However, that scroll area became quite large and unwieldy.
I reconsidered the approach: what if users could simply tap the text field to open a sheet for editing the text, color, and font? This would create a much cleaner interface.

The default sheet height was too tall for this use case. I initially went down a somewhat wasteful path of creating a custom sheet before discovering [this post](https://www.hackingwithswift.com/quick-start/swiftui/how-to-control-the-size-of-presented-views), which shows how to make sheets more appropriately sized.

As part of this redesign, I also decided to commit fully to iOS 26 and have the entire app inherit Liquid Glass styling, rather than trying to maintain backward compatibility with previous versions.​​​​​​​​​​​​​​​​