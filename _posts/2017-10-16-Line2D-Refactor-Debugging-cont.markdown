---
layout: post
title: "Line2D Refactor & Debugging"
date: 2017-10-16
categories: jekyll update
---

Tasks for 10/16/17:
1. debugging `matplotlib.lines.Line2D`
    * look at notes from last post

~~~
xy = STEP_LOOKUP_MAP[self.drawstyle](self.xy.T)
TypeError: <lambda>() missing 1 required positional argument: 'y'
~~~
This error has been reoccurring and I think I have an idea on how to get it fixed

**Speculation**: What if the way `Line2D` is being called in other modules affecting my implementation?
    * Checked `pyplot.py` and I have confirmed that `_traits.lines.Line2D` was imported properly
    * To answer my question, I will be looking through all other modules in MPL.

From `axis.py`:
~~~
axis.py line 431 function _get_tick1line testing l
l.linewidth 1.5
l.linestyle None
l.color C0
l.marker None
l.markersize 6.0
l.markeredgewidth None
l.markerfacecolor None
l.markerfacecoloralt none
l.fillstyle None
l.antialiased True
l.dash_capstyle butt
l.solid_capstyle projecting
l.dash_joinstyle round
l.solid_joinstyle round
l.pickradius 5
l.drawstyle default
l.markevery None
l.verticalOffset None
l.ind_offset 0
l.invalidx True
l.invalidy True
l.path Path(array([[ 0.,  0.],
       [ 1.,  0.],
       [ 1.,  1.],
       [ 1.,  0.]]), None)
l.transformed_path None
l.subslice False
l.x_filled None
l.dashSeq None
l.dashOffset None
l.us_dashSeq None
l.us_dashOffset None
~~~

From `axis.py`:
~~~
axis.py line 447 function _get_tick2line testing l
l.linewidth 1.5
l.linestyle None
l.color C0
l.marker None
l.markersize 6.0
l.markeredgewidth None
l.markerfacecolor None
l.markerfacecoloralt none
l.fillstyle None
l.antialiased True
l.dash_capstyle butt
l.solid_capstyle projecting
l.dash_joinstyle round
l.solid_joinstyle round
l.pickradius 5
l.drawstyle default
l.markevery None
l.verticalOffset None
l.ind_offset 0
l.invalidx True
l.invalidy True
l.path Path(array([[ 0.,  0.],
       [ 1.,  0.],
       [ 1.,  1.],
       [ 1.,  0.]]), None)
l.transformed_path None
l.subslice False
l.x_filled None
l.dashSeq None
l.dashOffset None
l.us_dashSeq None
l.us_dashOffset None
~~~

Testing in `ipython`
~~~
In [1]: from matplotlib._traits.lines import Line2D
   ...: line = Line2D(xdata=[0,1,2,3],ydata=[0,1,2,3])
   ...: print("line", line)
   ...: print("line.linewidth", line.linewidth)
   ...: print("line.linestyle", line.linestyle)
   ...: print("line.color", line.color)
   ...: print("line.marker", line.marker)
   ...: print("line.markersize", line.markersize)
   ...: print("line.markeredgewidth", line.markeredgewidth)
   ...: print("line.markerfacecolor", line.markerfacecolor)
   ...: print("line.markerfacecoloralt", line.markerfacecoloralt)
   ...: print("line.fillstyle", line.fillstyle)
   ...: print("line.antialiased", line.antialiased)
   ...: print("line.dash_capstyle", line.dash_capstyle)
   ...: print("line.solid_capstyle", line.solid_capstyle)
   ...: print("line.dash_joinstyle", line.dash_joinstyle)
   ...: print("line.solid_joinstyle", line.solid_joinstyle)
   ...: print("line.pickradius", line.pickradius)
   ...: print("line.drawstyle", line.drawstyle)
   ...: print("line.markevery", line.markevery)
   ...: print("line.verticalOffset", line.verticalOffset)
   ...: print("line.ind_offset", line.ind_offset)
   ...: print("line.invalidx", line.invalidx)
   ...: print("line.invalidy", line.invalidy)
   ...: print("line.path", line.path)
   ...: print("line.transformed_path", line.transformed_path)
   ...: print("line.subslice", line.subslice)
   ...: print("line.x_filled", line.x_filled)
   ...: print("line.dashSeq", line.dashSeq)
   ...: print("line.dashOffset", line.dashOffset)
   ...: print("line.us_dashSeq", line.us_dashSeq)
   ...: print("line.us_dashOffset", line.us_dashOffset)
a:  <matplotlib.artist.Artist object at 0x10f1499e8>
_traits/line.py line 377 xorig  []
_traits/line.py line 378 yorig  []
_traits/line.py line 379 x  []
_traits/line.py line 380 y []
_traits/line.py line 381 xy None
_traits/line.py line 480 function __init__ before set_data self.xy  None
_traits/line.py line 481 function __init__ before set_data self.x  []
_traits/line.py line 482 function __init__ before set_data self.y  []
_traits/line.py line 483 function __init__ before set_data xdata  [0, 1, 2, 3]
_traits/line.py line 484 function __init__ before set_data ydata  [0, 1, 2, 3]
_traits/line.py line 485 function __init__ setting the data here
_traits/line.py line 396 function set_data called set_data(xdata, ydata)
_traits/line.py line 402 function set_data x [0, 1, 2, 3]
_traits/line.py line 403 function set_data y [0, 1, 2, 3]
_traits/line.py line 414 function set_xdata called set_xdata
_traits/line.py line 425 function set_ydata called set_ydata
_traits/line.py line 487 function __init__ successfully set the data
_traits/line.py line 488 function __init__ after set_data self.xy  None
_traits/line.py line 489 function __init__ after set_data self.x  []
_traits/line.py line 490 function __init__ after set_data self.y  []
line Line2D()
line.linewidth 1.5
line.linestyle None
line.color C0
line.marker None
line.markersize 6.0
line.markeredgewidth None
line.markerfacecolor None
line.markerfacecoloralt none
line.fillstyle None
line.antialiased True
line.dash_capstyle butt
line.solid_capstyle projecting
line.dash_joinstyle round
line.solid_joinstyle round
line.pickradius 5
line.drawstyle default
line.markevery None
line.verticalOffset None
line.ind_offset 0
line.invalidx True
line.invalidy True
line.path Path(array([[ 0.,  0.],
       [ 1.,  0.],
       [ 1.,  1.],
       [ 1.,  0.]]), None)
line.transformed_path None
line.subslice False
line.x_filled None
line.dashSeq None
line.dashOffset None
line.us_dashSeq None
line.us_dashOffset None
~~~
