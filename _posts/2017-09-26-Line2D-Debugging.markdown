---
layout: post
title: "Line2D Debugging"
date: 2017-09-26
categories: jekyll update
---

Tasks:
1. Continue Debugging Line2D
2. Get Paul set up with proper materials to begin coding

~~~
#testing code in ipython
import matplotlib
from matplotlib._traits.artist import Artist
from matplotlib._traits.lines import Line2D
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.artist as baseArtist
a = baseArtist.Artist()
isinstance(a, matplotlib._traits.artist.Artist)
plt.plot([4, 3, 2, 1])
plt.ylabel('some numbers')
plt.show()
~~~

Let's see what happens after running this for the first time...

~~~
a:  <matplotlib.artist.Artist object at 0x1122e49b0>
matplotlib.artist b_artist:  <module 'matplotlib.artist' from '/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/artist.py'>
matplotlib.lines.Line2D <module 'matplotlib.lines' from '/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/lines.py'>
before b_Line2D.Line2D:  <class 'matplotlib.lines.Line2D'>
after b_Line2D.Line2D:  <class 'matplotlib._traits.lines.Line2D'>
Artist:  <class 'matplotlib._traits.artist.Artist'>
invalidx: cross validating True
invalidy: cross validating True
Artist:  <class 'matplotlib._traits.artist.Artist'>
invalidx: cross validating True
invalidy: cross validating True
Artist:  <class 'matplotlib._traits.artist.Artist'>
invalidx: cross validating True
invalidy: cross validating True
subslice: cross validating False
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
<ipython-input-1-d5aac2988273> in <module>()
      7 a = baseArtist.Artist()
      8 isinstance(a, matplotlib._traits.artist.Artist)
----> 9 plt.plot([4, 3, 2, 1])
     10 plt.ylabel('some numbers')
     11 plt.show()

~/Desktop/matplotlib/lib/matplotlib/pyplot.py in plot(*args, **kwargs)
   3240 @_autogen_docstring(Axes.plot)
   3241 def plot(*args, **kwargs):
-> 3242     ax = gca()
   3243     # Deprecated: allow callers to override the hold state
   3244     # by passing hold=True|False

~/Desktop/matplotlib/lib/matplotlib/pyplot.py in gca(**kwargs)
    972     matplotlib.figure.Figure.gca : The figure's gca method.
    973     """
--> 974     return gcf().gca(**kwargs)
    975
    976 # More ways of creating axes:

~/Desktop/matplotlib/lib/matplotlib/figure.py in gca(self, **kwargs)
   1597
   1598         # no axes found, so create one which spans the figure
-> 1599         return self.add_subplot(1, 1, 1, **kwargs)
   1600
   1601     def sca(self, a):

~/Desktop/matplotlib/lib/matplotlib/figure.py in add_subplot(self, *args, **kwargs)
   1056                     self._axstack.remove(ax)
   1057
-> 1058             a = subplot_class_factory(projection_class)(self, *args, **kwargs)
   1059
   1060         self._axstack.add(key, a)

~/Desktop/matplotlib/lib/matplotlib/axes/_subplots.py in __init__(self, fig, *args, **kwargs)
     71
     72         # _axes_class is set in the subplot_class_factory
---> 73         self._axes_class.__init__(self, fig, self.figbox, **kwargs)
     74
     75     def __reduce__(self):

~/Desktop/matplotlib/lib/matplotlib/axes/_base.py in __init__(self, fig, rect, facecolor, frameon, sharex, sharey, label, xscale, yscale, axisbg, **kwargs)
    516
    517         # this call may differ for non-sep axes, e.g., polar
--> 518         self._init_axis()
    519         if axisbg is not None and facecolor is not None:
    520             raise TypeError('Both axisbg and facecolor are not None. '

~/Desktop/matplotlib/lib/matplotlib/axes/_base.py in _init_axis(self)
    607     def _init_axis(self):
    608         "move this out of __init__ because non-separable axes don't use it"
--> 609         self.xaxis = maxis.XAxis(self)
    610         self.spines['bottom'].register_axis(self.xaxis)
    611         self.spines['top'].register_axis(self.xaxis)

~/Desktop/matplotlib/lib/matplotlib/axis.py in __init__(self, axes, pickradius)
    661         self._minor_tick_kw = dict()
    662
--> 663         self.cla()
    664         self._set_scale('linear')
    665

~/Desktop/matplotlib/lib/matplotlib/axis.py in cla(self)
    756         self._set_artist_props(self.label)
    757
--> 758         self.reset_ticks()
    759
    760         self.converter = None

~/Desktop/matplotlib/lib/matplotlib/axis.py in reset_ticks(self)
    770         del self.minorTicks[:]
    771
--> 772         self.majorTicks.extend([self._get_tick(major=True)])
    773         self.minorTicks.extend([self._get_tick(major=False)])
    774         self._lastNumMajorTicks = 1

~/Desktop/matplotlib/lib/matplotlib/axis.py in _get_tick(self, major)
   1731         else:
   1732             tick_kw = self._minor_tick_kw
-> 1733         return XTick(self.axes, 0, '', major=major, **tick_kw)
   1734
   1735     def _get_label(self):

~/Desktop/matplotlib/lib/matplotlib/axis.py in __init__(self, axes, loc, label, size, width, color, tickdir, pad, labelsize, labelcolor, zorder, gridOn, tick1On, tick2On, label1On, label2On, major, labelrotation)
    157         self.tick1line = self._get_tick1line()
    158         self.tick2line = self._get_tick2line()
--> 159         self.gridline = self._get_gridline()
    160
    161         self.label1 = self._get_text1()

~/Desktop/matplotlib/lib/matplotlib/axis.py in _get_gridline(self)
    455                           markersize=0)
    456         l.set_transform(self.axes.get_xaxis_transform(which='grid'))
--> 457         l.get_path()._interpolation_steps = GRIDLINE_INTERPOLATION_STEPS
    458         # l.path._interpolation_steps = GRIDLINE_INTERPOLATION_STEPS
    459

~/Desktop/matplotlib/lib/matplotlib/_traits/lines.py in get_path(self)
   1449         """
   1450         if self.invalidy or self.invalidx:
-> 1451             self.recache()
   1452         return self.path
   1453

~/Desktop/matplotlib/lib/matplotlib/_traits/lines.py in recache(self, always)
   1204         else:
   1205             interpolation_steps = 1
-> 1206         xy = STEP_LOOKUP_MAP[self.drawstyle](*self.xy.T)
   1207         self.path = Path(np.asarray(xy).T,
   1208                           _interpolation_steps=interpolation_steps)

KeyError: None
~~~
So this did not work...
