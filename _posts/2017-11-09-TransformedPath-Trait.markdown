---
layout: post
title: "TransformedPath Trait cont."
date: 2017-11-09
categories: jekyll update
---

Tasks for 11/09/17:
1. debugging `matplotlib.lines.Line2D`
    * look at notes from last posts
2. Create a `TransformedPathTrait` to be used as `transformed_path` attribute in `Line2D`


Tester Lines Output:
~~~
isinstance(proposal.value, Path): True
isinstance(proposal.value, TransformedPath): True
_traits/lines.py line 925 self.transformed_path:  <matplotlib.transforms.TransformedPath object at 0x1193d5f98>
_traits/lines.py line 929 transf_path:  <matplotlib.transforms.TransformedPath object at 0x1193d5f98>
~~~


Error Currently Working On:
~~~
self.markerfacecolor:  None
Exception in Tkinter callback
Traceback (most recent call last):
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/colors.py", line 142, in to_rgba
    rgba = _colors_full_map.cache[c, alpha]
KeyError: (None, None)

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
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/_traits/lines.py", line 1017, in draw
    rgbaFace = self._get_rgba_face()
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/_traits/lines.py", line 1168, in _get_rgba_face
    rgbaFace = mcolors.to_rgba(facecolor, self.alpha)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/colors.py", line 144, in to_rgba
    rgba = _to_rgba_no_colorcycle(c, alpha)
  File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/colors.py", line 195, in _to_rgba_no_colorcycle
    raise ValueError("Invalid RGBA argument: {!r}".format(orig_c))
ValueError: Invalid RGBA argument: None
~~~


Let's see if this works:
~~~
color=Union([Unicode(), Float(), Tuple()], allow_none=False, default_value='C0')
~~~

To tackle the `None` problems I've been having; `allow_none=True` were all switched to `allow_none=False`
- I will not allow falsehood in this code
