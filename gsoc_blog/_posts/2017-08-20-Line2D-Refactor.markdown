---
layout: post
title: "Line2D Refactor"
date: 2017-08-20
categories: jekyll update
---

Tasks for 8/20/17:
1. refactor `matplotlib.lines.Line2D`
    * look at previous notes
    * start refactor `matplotlib.lines.Line2D`

Notes:
~~~
xdata
    Set the data np.array for x
    ACCEPTS: 1D array
    Instance('numpy.array', allow_none=True,default_value=True) # not sure about this line

ydata
    Set the data np.array for y
    ACCEPTS: 1D array
    Instance('numpy.array', allow_none=True,default_value=True) # not sure about this line

linewidth=None  # all Nones default to rc
    Set the line width in points
    ACCEPTS: float value in points
    Float(allow_none=True, default_value=None)

linestyle=None
    ACCEPTS: ['solid' | 'dashed', 'dashdot', 'dotted' | (offset, on-off-dash-seq) | ``'-'`` | ``'--'`` | ``'-.'`` | ``':'`` | ``'None'`` | ``' '`` | ``''``]
    Not Sure how to go about this one.
    Maybe an instance of Text?

color=None
    ACCEPTS: any matplotlib color
    Is color an Instance of matplotlib.Color, numpy.array or an Int?

marker=None
    Set the line marker
    ACCEPTS: :mod:`A valid marker style <matplotlib.markers>`

markersize=None
    ACCEPTS: float

markeredgewidth=None
    ACCEPTS: float value in points
    is this an array?

markeredgecolor=None
    ACCEPTS: any matplotlib color

markerfacecolor=None
    ACCEPTS: any matplotlib color

markerfacecoloralt='none'
    Set the alternate marker face `color`.
    ACCEPTS: any matplotlib color

fillstyle=None
    Set the marker fill style; 'full' means fill the whole marker.
    'none' means no filling; other options are for half-filled markers.
    ACCEPTS: ['full' | 'left' | 'right' | 'bottom' | 'top' | 'none']

antialiased=None
    True if line should be drawing with antialiased rendering
    ACCEPTS: [True | False]
    in the original line2d module, antialiased is set to None but in set_antialiased the only values accepted are True and False; for this I will set to False at first

dash_capstyle=None
    Set the cap style for dashed linestyles
    ACCEPTS: ['butt' | 'round' | 'projecting']  

solid_capstyle=None
    Set the cap style for solid linestyles
    ACCEPTS: ['butt' | 'round' |  'projecting']

dash_joinstyle=None
    Set the join style for dashed linestyles
    ACCEPTS: ['miter' | 'round' | 'bevel']

solid_joinstyle=None
    Set the join style for solid linestyles
    ACCEPTS: ['miter' | 'round' | 'bevel']

pickradius=5
    Sets the pick radius used for containment tests
    ACCEPTS: float distance in points
    Int(allow_none=True, default_value=5)

drawstyle=None
    Set the drawstyle of the plot 'default' connects the points with lines. The steps variants produce step-plots. 'steps' is equivalent to 'steps-pre' and is maintained for backward-compatibility.
    ACCEPTS: ['default' | 'steps' | 'steps-pre' | 'steps-mid' | 'steps-post']

markevery=None
    Set the markevery property to subsample the plot when using markers. e.g., if `every=5`, every 5-th marker will be plotted.
    ACCEPTS: [None | int | length-2 tuple of int | slice | list/array of int | float | length-2 tuple of float]

**kwargs
    Not sure how to go about **kwargs in terms of traits
~~~
