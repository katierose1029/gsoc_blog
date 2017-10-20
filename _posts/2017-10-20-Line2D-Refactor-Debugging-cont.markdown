---
layout: post
title: "Line2D Refactor & Debugging"
date: 2017-10-20
categories: jekyll update
---

Tasks for 10/20/17:
1. debugging `matplotlib.lines.Line2D`
    * look at notes from last posts

Current Error I am fixing:
~~~
File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/_traits/lines.py", line 1063, in draw
  if self.lineStyles[self.linestyle] != '_draw_nothing':
~~~

[Paul's Commits][pc]

[pc]:https://github.com/Neminem1203/matplotlib/commits/figure-traitlets-dev
