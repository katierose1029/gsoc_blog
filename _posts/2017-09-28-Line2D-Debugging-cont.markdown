---
layout: post
title: "Line2D Debugging cont."
date: 2017-09-28
categories: jekyll update
---

Tasks for 9/28/17:
1. Clean up code to send to Ryan: need another set of eyes to determine where the `None` is coming from
2. Get Paul set up to code.

Notes:

**Path may have to be it's own trait!!!**
* for the same reasons on how we handle `matplotlib.transforms.Transform`
    * `None`
* could also have been a problem because `Path` inherits from `object` as opposed to `Artist`

**The other problem could be that xy may have never been set to any values**
