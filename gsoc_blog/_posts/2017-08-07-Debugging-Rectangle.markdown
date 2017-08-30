---
layout: post
title: "Rectangle Debugging"
date: 2017-08-07
categories: jekyll update
---

Tasks for 8/07/17:
1. Debugging `Rectangle` `hold_trait_notifications` error

**Error Traceback:**
~~~
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-2-5f4aaac063ba> in <module>()
----> 1 plt.plot([4, 3, 2, 1])
      2 plt.ylabel('some numbers')
      3 plt.show()

~/Desktop/matplotlib/lib/matplotlib/pyplot.py in plot(*args, **kwargs)
   3235 @_autogen_docstring(Axes.plot)
   3236 def plot(*args, **kwargs):
-> 3237     ax = gca()
   3238     # Deprecated: allow callers to override the hold state
   3239     # by passing hold=True|False

~/Desktop/matplotlib/lib/matplotlib/pyplot.py in gca(**kwargs)
    967     matplotlib.figure.Figure.gca : The figure's gca method.
    968     """
--> 969     return gcf().gca(**kwargs)
    970
    971 # More ways of creating axes:

~/Desktop/matplotlib/lib/matplotlib/pyplot.py in gcf()
    596         return figManager.canvas.figure
    597     else:
--> 598         return figure()
    599
    600

~/Desktop/matplotlib/lib/matplotlib/pyplot.py in figure(num, figsize, dpi, facecolor, edgecolor, frameon, FigureClass, clear, **kwargs)
    542                                         frameon=frameon,
    543                                         FigureClass=FigureClass,
--> 544                                         **kwargs)
    545
    546         if figLabel:

~/Desktop/matplotlib/lib/matplotlib/backends/backend_tkagg.py in new_figure_manager(num, *args, **kwargs)
     77     """
     78     FigureClass = kwargs.pop('FigureClass', Figure)
---> 79     figure = FigureClass(*args, **kwargs)
     80     return new_figure_manager_given_figure(num, figure)
     81

~/Desktop/matplotlib/lib/matplotlib/figure.py in __init__(self, figsize, dpi, facecolor, edgecolor, linewidth, frameon, subplotpars, tight_layout)
    342         self.patch = Rectangle(
    343             xy=(0, 0), width=1, height=1,
--> 344             facecolor=facecolor, edgecolor=edgecolor, linewidth=linewidth)
    345         self._set_artist_props(self.patch)
    346         self.patch.set_aa(False)

~/Desktop/matplotlib/lib/matplotlib/patches.py in __init__(self, xy, width, height, angle, **kwargs)
    687         """
    688
--> 689         Patch.__init__(self, **kwargs)
    690
    691         self._x = float(xy[0])

~/Desktop/matplotlib/lib/matplotlib/patches.py in __init__(self, edgecolor, facecolor, color, linewidth, linestyle, antialiased, hatch, fill, capstyle, joinstyle, **kwargs)
    102         %(Patch)s
    103         """
--> 104         artist.Artist.__init__(self)
    105
    106         if linewidth is None:

~/anaconda3/envs/mpl-testing/lib/python3.6/site-packages/traitlets/traitlets.py in __init__(self, *args, **kwargs)
    992         super_args = args
    993         super_kwargs = {}
--> 994         with self.hold_trait_notifications():
    995             for key, value in kwargs.items():
    996                 if self.has_trait(key):

AttributeError: 'Rectangle' object has no attribute 'hold_trait_notifications'
~~~

Mentor Mentions:
* problem isn't with traits
    * problem is inheritance/construction of the Rectangle
* which `Rectangle` am I importing?
    * rectangle from `_traits` or base library?

~~~
In [4]: Rectangle
Out[4]: matplotlib.patches.Rectangle
~~~

* with this knowledge maybe i can try making an rectangle instance via traits?
* used following link to help me draw mpl rectangle
    * [Rectangle Example][rex]

~~~
[mpl-testing][KaitlynChait][~] ➤  ipython
Python 3.6.2 |Continuum Analytics, Inc.| (default, Jul 20 2017, 13:14:59)
Type 'copyright', 'credits' or 'license' for more information
IPython 6.1.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]: import matplotlib
   ...: from matplotlib._traits.artist import Artist
   ...: from matplotlib._traits.traits import *
   ...: import numpy as np
   ...: import matplotlib.pyplot as plt
imported Ractangle successfully

In [2]: from matplotlib._traits.artist import Rectangle

In [3]: a = Artist()
stale_callback: observed a change from True to None
eventson: cross validating False

In [4]: left, width = .25, .5
   ...: bottom, height = .25, .5
   ...: right = left + width
   ...: top = bottom + height

In [5]: r = Rectangle((left, bottom), width, height)
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-5-3aa44981d294> in <module>()
----> 1 r = Rectangle((left, bottom), width, height)

~/Desktop/matplotlib/lib/matplotlib/patches.py in __init__(self, xy, width, height, angle, **kwargs)
    687         """
    688
--> 689         Patch.__init__(self, **kwargs)
    690
    691         self._x = float(xy[0])

~/Desktop/matplotlib/lib/matplotlib/patches.py in __init__(self, edgecolor, facecolor, color, linewidth, linestyle, antialiased, hatch, fill, capstyle, joinstyle, **kwargs)
    102         %(Patch)s
    103         """
--> 104         artist.Artist.__init__(self)
    105
    106         if linewidth is None:

~/anaconda3/envs/mpl-testing/lib/python3.6/site-packages/traitlets/traitlets.py in __init__(self, *args, **kwargs)
    992         super_args = args
    993         super_kwargs = {}
--> 994         with self.hold_trait_notifications():
    995             for key, value in kwargs.items():
    996                 if self.has_trait(key):

AttributeError: 'Rectangle' object has no attribute 'hold_trait_notifications'
~~~

~~~
In [6]: from matplotlib.patches import Rectangle

In [7]: r = Rectangle((left, bottom), width, height)
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-7-3aa44981d294> in <module>()
----> 1 r = Rectangle((left, bottom), width, height)

~/Desktop/matplotlib/lib/matplotlib/patches.py in __init__(self, xy, width, height, angle, **kwargs)
    687         """
    688
--> 689         Patch.__init__(self, **kwargs)
    690
    691         self._x = float(xy[0])

~/Desktop/matplotlib/lib/matplotlib/patches.py in __init__(self, edgecolor, facecolor, color, linewidth, linestyle, antialiased, hatch, fill, capstyle, joinstyle, **kwargs)
    102         %(Patch)s
    103         """
--> 104         artist.Artist.__init__(self)
    105
    106         if linewidth is None:

~/anaconda3/envs/mpl-testing/lib/python3.6/site-packages/traitlets/traitlets.py in __init__(self, *args, **kwargs)
    992         super_args = args
    993         super_kwargs = {}
--> 994         with self.hold_trait_notifications():
    995             for key, value in kwargs.items():
    996                 if self.has_trait(key):

AttributeError: 'Rectangle' object has no attribute 'hold_trait_notifications'

In [8]: Rectangle
Out[8]: matplotlib.patches.Rectangle
~~~

* **Good News Everyone, my mentor knows what is going on!!**
    * rectangle isn't using `super`
    * his word exactly: The object referred to by self when being passed to `Artist.__init__` is not an instance of `_traits.artist.Artist` and thus does not have `hold_trait_notifications`
    * monkey patching is most likely what is causing this problem

Questions for Mentor later:
1. Due to the underscore convention do you also think there is no access to `_traits/artist`?
    * attempt: `_traits` -> `traits`
        * this attempt did not work
2. Monkey Patching: checking correctness of Patching
~~~
_artist.Artist:  <class 'matplotlib.artist.Artist'>
traits: _artist.Artist:  <class 'matplotlib._traits.artist.Artist'>
~~~
    * in `_traits/artist` does the `_artist` have a true underscore convention?
* Note: making a successful `__init__(self)` will allow `_traitlets.artist.Artist` to be used/tested in other scripts where an initiation occurs



[rex]:https://matplotlib.org/devdocs/gallery/pyplots/text_layout.html#sphx-glr-gallery-pyplots-text-layout-py
