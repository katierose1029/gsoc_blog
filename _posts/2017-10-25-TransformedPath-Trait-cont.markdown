---
layout: post
title: "TransformedPath Trait"
date: 2017-10-25
categories: jekyll update
---

Tasks for 10/25/17:
1. debugging `matplotlib.lines.Line2D`
    * look at notes from last posts
2. Create a `TransformedPathTrait` to be used as `transformed_path` attribute in `Line2D`

After cleaning up this code yesterday and implementing the correct import statements; there was still an issue with the value of `transformed_path` being `None`

Here is the error message returned
~~~
In [1]: import matplotlib
   ...: from matplotlib._traits.artist import Artist
   ...: from matplotlib._traits.lines import Line2D
   ...: import numpy as np
   ...: import matplotlib.pyplot as plt
   ...: plt.plot([4, 3, 2, 1])
   ...: plt.ylabel('some numbers')
   ...: plt.show()
a:  <matplotlib.artist.Artist object at 0x107457a20>
_traits/lines.py line 925 self.transformed_path:  None
_traits/lines.py line 929 transf_path:  None
Exception in Tkinter callback
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
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/_traits/lines.py", line 943, in draw
    tpath, affine = transf_path.get_transformed_path_and_affine()
AttributeError: 'NoneType' object has no attribute 'get_transformed_path_and_affine'
~~~
