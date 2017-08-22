---
layout: post
title: "Line2D Refactor"
date: 2017-08-22
categories: jekyll update
---

Tasks for 8/22/17:
1. refactor `matplotlib.lines.Line2D`
    * look at previous notes

All Attributes:
    * Note not all of these will be used but these are from original `__init__` function
~~~
xdata=Instance('numpy.array', allow_none=True,default_value=True) not sure about this line
ydata=Instance('numpy.array', allow_none=True,default_value=True) not sure about this line
linewidth=Float(allow_none=True, default_value=None)
linestyle=

color=
marker=Instance('matplotlib.markers',allow_none=True, default_value=None)
markersize=Float(allow_none=True,default_value=True)
markeredgewidth=
markerfacecolor = None
markerfacecoloralt = None
fillstyle=
antialiased=Bool(default_value=False)
dash_capstyle=
solid_capstyle=
dash_joinstyle=
solid_joinstyle=
pickradius=Int(allow_none=True, default_value=5)
drawstyle=
markevery=
verticalOffset = None
ind_offset = 0


xorig = np.asarray([])
yorig = np.asarray([])
invalidx = True
invalidy = True
x = None
y = None
xy = None
path = None
transformed_path = None
subslice = False
x_filled = None  used in subslicing; only x is needed
set_data(xdata, ydata)

scaled dash + offset
dashSeq = None
dashOffset = 0
unscaled dash + offset
this is needed scaling the dash pattern by linewidth
us_dashSeq = None
us_dashOffset = 0
~~~
