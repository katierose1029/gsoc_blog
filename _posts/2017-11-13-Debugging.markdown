---
layout: post
title: "Debugging"
date: 2017-11-13
categories: jekyll update
---

Tasks for 11/13/17:
1. debugging `matplotlib.lines.Line2D`
    * look at notes from last posts

Current Error:
~~~
In [1]: import matplotlib
   ...: from matplotlib._traits.artist import Artist
   ...: from matplotlib._traits.lines import Line2D
   ...: import numpy as np
   ...: import matplotlib.pyplot as plt
   ...: plt.plot([4, 3, 2, 1])
   ...: plt.ylabel('some numbers')
   ...: plt.show()
a:  <matplotlib.artist.Artist object at 0x1096d3898>
color:  <traitlets.traitlets.Unicode object at 0x1095bc2b0>
_traits/lines.py line 925 self.transformed_path:  <matplotlib.transforms.TransformedPath object at 0x109dbe240>
_traits/lines.py line 929 transf_path:  <matplotlib.transforms.TransformedPath object at 0x109dbe240>
self.marker:  None
self.markersize:  6.0
facecolor:
Exception in Tkinter callback
Traceback (most recent call last):
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/colors.py", line 142, in to_rgba
    rgba = _colors_full_map.cache[c, alpha]
KeyError: ('', None)

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/KaitlynChait/anaconda3/envs/mpl-testing/lib/python3.6/tkinter/__init__.py", line 1699, in __call__
    return self.func(*args)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/backends/backend_tkagg.py", line 283, in resize
    self.show()
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/backends/backend_tkagg.py", line 354, in draw
    FigureCanvasAgg.draw(self)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/backends/backend_agg.py", line 444, in draw
    self.figure.draw(self.renderer)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/artist.py", line 76, in draw_wrapper
    return draw(artist, renderer, *args, **kwargs)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/figure.py", line 1283, in draw
    renderer, self, artists, self.suppressComposite)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/image.py", line 143, in _draw_list_compositing_images
    a.draw(renderer)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/artist.py", line 76, in draw_wrapper
    return draw(artist, renderer, *args, **kwargs)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/axes/_base.py", line 2392, in draw
    mimage._draw_list_compositing_images(renderer, self, artists)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/image.py", line 143, in _draw_list_compositing_images
    a.draw(renderer)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/artist.py", line 76, in draw_wrapper
    return draw(artist, renderer, *args, **kwargs)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/axis.py", line 1201, in draw
    tick.draw(renderer)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/artist.py", line 76, in draw_wrapper
    return draw(artist, renderer, *args, **kwargs)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/axis.py", line 268, in draw
    self.tick1line.draw(renderer)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/_traits/artist.py", line 66, in draw_wrapper
    return draw(artist, renderer, *args, **kwargs)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/_traits/lines.py", line 1019, in draw
    rgbaFace = self._get_rgba_face()
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/_traits/lines.py", line 1169, in _get_rgba_face
    rgbaFace = mcolors.to_rgba(facecolor, self.alpha)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/colors.py", line 144, in to_rgba
    rgba = _to_rgba_no_colorcycle(c, alpha)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/colors.py", line 188, in _to_rgba_no_colorcycle
    raise ValueError("Invalid RGBA argument: {!r}".format(orig_c))
ValueError: Invalid RGBA argument: ''\
~~~
