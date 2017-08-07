---
layout: post
title: "Rectangle Debugging"
date: 2017-08-07
categories: jekyll update
---

Tasks for 8/07/17:
1. Debugging Rectangle hold_trait_notifications error

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
    * which *Rectangle* am I importing?
        * rectangle from *_traits* or base library?
