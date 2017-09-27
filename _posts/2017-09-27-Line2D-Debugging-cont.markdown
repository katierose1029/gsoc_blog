---
layout: post
title: "Line2D Debugging"
date: 2017-09-27
categories: jekyll update
---

Tasks for 9/27/17:
1. Continue to debug & test Line2D
2. get Paul set up -> meant to do this yesterday but I had some health problems

~~~
#testing code in ipython
import matplotlib
from matplotlib._traits.artist import Artist
from matplotlib._traits.lines import Line2D
import numpy as np
import matplotlib.pyplot as plt
plt.plot([4, 3, 2, 1])
plt.ylabel('some numbers')
plt.show()
~~~

* commented out print statements
    * runs faster
    * commented out observe functions not needed because only print statement
        * any observe function that altered the value of stale did not change
