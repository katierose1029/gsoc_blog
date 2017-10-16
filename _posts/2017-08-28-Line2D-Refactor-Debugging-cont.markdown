---
layout: post
title: "Line2D Refactor & Debugging"
date: 2017-08-28
categories: jekyll update
---

Tasks for 8/28/17:
1. refactor & debugging `matplotlib.lines.Line2D`
2. GSOC Final Evaluation
    * Final work has to be handed in by tomorrow


~~~
# Artist.axes.fset(self, ax)
Artist.axes = ax #in reference to Artist with traitlets
~~~
    * may cause an error

* end of the axes function was causing error
    * my own dumb copy and paste error

**There seems to be a lot of import errors at this point**

*matplotlib.axis**
~~~
# l.get_path()._interpolation_steps = GRIDLINE_INTERPOLATION_STEPS
l.path._interpolation_steps = GRIDLINE_INTERPOLATION_STEPS
~~~
    * this did not work at all
