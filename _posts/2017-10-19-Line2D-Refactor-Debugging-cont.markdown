---
layout: post
title: "Line2D Refactor & Debugging"
date: 2017-10-19
categories: jekyll update
---

Tasks for 10/19/17:
1. debugging `matplotlib.lines.Line2D`
    * look at notes from last posts

~~~
xy = STEP_LOOKUP_MAP[self.drawstyle](*self.xy.T) # this line is correct and does not cause any errors
xy = STEP_LOOKUP_MAP[self.drawstyle](self.xy.T) # this line caused lambda error
~~~
[Unpacking Argument Lists][ual]

Note: I also commented out some print statements because they were causing errors

[ual]:https://docs.python.org/3/tutorial/controlflow.html#unpacking-argument-lists
