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
xdata=Instance('numpy.array', allow_none=True,default_value=True) #not sure about this line

ydata=Instance('numpy.array', allow_none=True,default_value=True) #not sure about this line

linewidth=Float(allow_none=True, default_value=None)

linestyle=Instance('matplotlib.text.Text', allow_none=True, default_value=None)

color=Unicode(allow_none=True, default_value=None)
#color=Instance('matplotlib.text.Text', allow_none=True,default_value=None)

marker=Instance('matplotlib.markers',allow_none=True, default_value=None)

markersize=Float(allow_none=True,default_value=True)

markeredgewidth=Float(allow_none=True,default_value=None)

# same for color because I am not sure if the color is Unicode or Python String; assume Unicode first for testing
markerfacecolor=Unicode(allow_none=True, default_value=None)
#markerfacecolor=Instance('matplotlib.text.Text', allow_none=True,default_value=None)

# same applies for the alternative face color
markerfacecoloralt=Unicode(allow_none=True, default_value=None)
#markerfacecoloralt=Instance('matplotlib.text.Text', allow_none=True,default_value=None)

# this gets passed into marker so I want to assume same for color however only accepts the following strings: ['full' | 'left' | 'right' | 'bottom' | 'top' | 'none']
fillstyle=Unicode(allow_none=True, default_value=None)
# fillstyle=Instance('matplotlib.text.Text', allow_none=True,default_value=None)
antialiased=Bool(default_value=False)

# accepts: ['butt' | 'round' | 'projecting']
dash_capstyle=Unicode(allow_none=True, default_value=None)
# dash_capstyle=Instance('matplotlib.text.Text', allow_none=True,default_value=None)

# accepts: ['butt' | 'round' | 'projecting']
solid_capstyle=Unicode(allow_none=True, default_value=None)
# solid_capstyle=Instance('matplotlib.text.Text', allow_none=True,default_value=None)

# accepts: ['miter' | 'round' | 'bevel']
dash_joinstyle=Unicode(allow_none=True, default_value=None)
# dash_joinstyle=Instance('matplotlib.text.Text', allow_none=True,default_value=None)

# accepts: ['miter' | 'round' | 'bevel']
solid_joinstyle=Unicode(allow_none=True, default_value=None)
# solid_joinstyle=Instance('matplotlib.text.Text', allow_none=True,default_value=None)

pickradius=Int(allow_none=True, default_value=5)

# accepts: ['default' | 'steps' | 'steps-pre' | 'steps-mid' |
          'steps-post']
drawstyle=Unicode(allow_none=True, default_value=None)
# drawstyle=Instance('matplotlib.text.Text', allow_none=True,default_value=None)

# for this one I want to attempt at using the ANY trait
markevery=Any(allow_none=True, default_value=None)

#only found once in the original lines code so not sure what to do with this
verticalOffset = None

ind_offset = Int(allow_none=True,default_value=0)
~~~
