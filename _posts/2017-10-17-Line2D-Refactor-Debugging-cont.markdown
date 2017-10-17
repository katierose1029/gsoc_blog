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
*

Trying out new testing code 
~~~
import numpy as np
import matplotlib.pyplot as plt
from matplotlib._traits.artist import Artist
from matplotlib._traits.lines import Line2D

x = np.arange(0, 5, 0.1);
y = np.sin(x)
plt.plot(x, y)
~~~
