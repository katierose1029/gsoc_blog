---
layout: post
title: "On to the Next Task"
date: 2017-08-16
categories: jekyll update
---

Tasks for 8/16/17:
1. Look into the next set of tasks for project

**Using this block of code in Ipython I was able to create a figure using the refactored `Artist` module**
~~~
import matplotlib
from matplotlib._traits.artist import Artist
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.artist as baseArtist
a = baseArtist.Artist()
isinstance(a, matplotlib._traits.artist.Artist)
plt.plot([4, 3, 2, 1])
plt.ylabel('some numbers')
plt.show()
~~~

~~~
Exception in Tkinter callback
Traceback (most recent call last):
  File "/Users/KaitlynChait/anaconda3/envs/mpl-testing/lib/python3.6/tkinter/__init__.py", line 1699, in __call__
    return self.func(*args)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/backends/backend_tkagg.py", line 405, in button_press_event
    FigureCanvasBase.button_press_event(self, x, y, num, dblclick=dblclick, guiEvent=event)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/backend_bases.py", line 1878, in button_press_event
    self.callbacks.process(s, mouseevent)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/cbook/__init__.py", line 365, in process
    proxy(*args, **kwargs)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/cbook/__init__.py", line 227, in __call__
    return mtd(*args, **kwargs)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/backend_bases.py", line 1781, in pick
    self.figure.pick(mouseevent)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/_traits/artist.py", line 969, in pick
    for a in self.contains:
TypeError: 'method' object is not iterable
~~~
    * keep note of this incase this becomes and issue
