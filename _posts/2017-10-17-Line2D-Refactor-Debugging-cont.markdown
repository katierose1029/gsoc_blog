---
layout: post
title: "Line2D Refactor & Debugging"
date: 2017-10-17
categories: jekyll update
---

Tasks for 10/17/17:
1. debugging `matplotlib.lines.Line2D`
    * look at notes from last posts
2. Meeting with Professor at 4:25 - 4:45

Notes for Meeting:
* Debugging is not complete
* Figure has been drawn with no line
* mention lambda error


Trying out new testing code:
~~~
import matplotlib
import numpy as np
import matplotlib.pyplot as plt
from matplotlib._traits.artist import Artist
from matplotlib._traits.lines import Line2D

x = np.arange(0, 5, 0.1);
y = np.sin(x)
plt.plot(x, y)
~~~

For science, I am determining whether or not `Path` has a default value
~~~
In [1]: from matplotlib.path import Path

In [2]: p = Path()
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-2-c0d85f7e4728> in <module>()
----> 1 p = Path()

TypeError: __init__() missing 1 required positional argument: 'vertices'
~~~
