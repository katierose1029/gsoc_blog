---
layout: post
title: "Line2D Refactor"
date: 2017-08-21
categories: jekyll update
---

Tasks for 8/21/17:
1. refactor `matplotlib.lines.Line2D`
    * look at previous notes

Other Attributes not accounted for:
~~~
# scaled dash + offset
# dashSeq = None
# dashOffset = 0
# unscaled dash + offset
# this is needed scaling the dash pattern by linewidth
# us_dashSeq = None
# us_dashOffset = 0
~~~
