---
layout: post
title: "Determining None cont."
date: 2017-10-09
categories: jekyll update
---

Tasks for 10/09/17:
1. Determine why `None` is being returned at the point in which it is?


~~~
#New Testing Code
from matplotlib._traits.lines import Line2D
line = Line2D(xdata=[0,1,2,3],ydata=[0,1,2,3])
print("line", line)
print("line.x", line.x)
print("line.y", line.y)
print("line.xy", line.xy)
print("line.linewidth", line.linewidth)
print("line.linestyle", line.linestyle)
print("line.color", line.color)
print("line.marker", line.marker)
print("line.markersize", line.markersize)
print("line.markeredgewidth", line.markeredgewidth)
print("line.markerfacecolor", line.markerfacecolor)
print("line.markerfacecoloralt", line.markerfacecoloralt)
print("line.fillstyle", line.fillstyle)
print("line.antialiased", line.antialiased)
print("line.dash_capstyle", line.dash_capstyle)
print("line.solid_capstyle", line.solid_capstyle)
print("line.dash_joinstyle", line.dash_joinstyle)
print("line.solid_joinstyle", line.solid_joinstyle)
print("line.pickradius", line.pickradius)
print("line.drawstyle", line.drawstyle)
print("line.markevery", line.markevery)
print("line.verticalOffset", line.verticalOffset)
print("line.ind_offset", line.ind_offset)
print("line.invalidx", line.invalidx)
print("line.invalidy", line.invalidy)
print("line.path", line.path)
print("line.transformed_path", line.transformed_path)
print("line.subslice", line.subslice)
print("line.x_filled", line.x_filled)
print("line.dashSeq", line.dashSeq)
print("line.dashOffset", line.dashOffset)
print("line.us_dashSeq", line.us_dashSeq)
print("line.us_dashOffset", line.us_dashOffset)
print("line.xdata", line.xdata)
print("line.ydata", line.ydata)
~~~


~~~
(_traits.lines.py lines 1181 - 1203)
#for testing, I want to catch the NONE error

    def set_xdata(self, x):
        """
        Set the data np.array for x

        ACCEPTS: 1D array
        """
        self._xorig = x
        self._invalidx = True
        self.stale = True

    def set_ydata(self, y):
        """
        Set the data np.array for y

        ACCEPTS: 1D array
        """
        self._yorig = y
        self._invalidy = True
        self.stale = True

#
~~~
    * note the way that this is "caught" by the interpreter is funny and if i place these functions, along with set_data, this will run properly
    * placed lines 356 - 388
