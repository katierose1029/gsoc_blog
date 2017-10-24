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
    * This seems to have worked

**I am attempting to create xdata & ydata as traits.Type**

**trying to figure out where xorig came from**
* not in base lines class

**also I cleaned up code:**
* got rid of default & observe functions I did not need

~~~
In [1]: from matplotlib._traits.lines import Line2D
   ...: line = Line2D(xdata=[0,1,2,3],ydata=[0,1,2,3])
   ...: print("line", line)
   ...: print("line.x", line.x)
   ...: print("line.y", line.y)
   ...: print("line.xy", line.xy)
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
   ...: print("line.xdata", line.xdata)
   ...: print("line.ydata", line.ydata)
a:  <matplotlib.artist.Artist object at 0x10ede1048>
setting the data here
called set_data(xdata, ydata)
called set_xdata
---------------------------------------------------------------------------
TraitError                                Traceback (most recent call last)
<ipython-input-1-625c47f22ae8> in <module>()
      1 from matplotlib._traits.lines import Line2D
----> 2 line = Line2D(xdata=[0,1,2,3],ydata=[0,1,2,3])
      3 print("line", line)
      4 print("line.x", line.x)
      5 print("line.y", line.y)

~/Desktop/matplotlib/lib/matplotlib/_traits/lines.py in __init__(self, xdata, ydata, linewidth, linestyle, color, marker, markersize, markeredgewidth, markeredgecolor, markerfacecolor, markerfacecoloralt, fillstyle, antialiased, dash_capstyle, solid_capstyle, dash_joinstyle, solid_joinstyle, pickradius, drawstyle, markevery, **kwargs)
    445
    446         print("setting the data here")
--> 447         self.set_data(xdata, ydata)
    448         print("successfully set the data")
    449

~/Desktop/matplotlib/lib/matplotlib/_traits/lines.py in set_data(self, *args)
    375             x, y = args
    376
--> 377         self.set_xdata(x)
    378         self.set_ydata(y)
    379

~/Desktop/matplotlib/lib/matplotlib/_traits/lines.py in set_xdata(self, x)
    385         """
    386         print("called set_xdata")
--> 387         self.xorig = x
    388         self.invalidx = True
    389         self.stale = True

~/anaconda3/envs/mpl-testing/lib/python3.6/site-packages/traitlets/traitlets.py in __set__(self, obj, value)
    583             raise TraitError('The "%s" trait is read-only.' % self.name)
    584         else:
--> 585             self.set(obj, value)
    586
    587     def _validate(self, obj, value):

~/anaconda3/envs/mpl-testing/lib/python3.6/site-packages/traitlets/traitlets.py in set(self, obj, value)
    557
    558     def set(self, obj, value):
--> 559         new_value = self._validate(obj, value)
    560         try:
    561             old_value = obj._trait_values[self.name]

~/anaconda3/envs/mpl-testing/lib/python3.6/site-packages/traitlets/traitlets.py in _validate(self, obj, value)
    589             return value
    590         if hasattr(self, 'validate'):
--> 591             value = self.validate(obj, value)
    592         if obj._cross_validation_lock is False:
    593             value = self._cross_validate(obj, value)

~/anaconda3/envs/mpl-testing/lib/python3.6/site-packages/traitlets/traitlets.py in validate(self, obj, value)
   1584             pass
   1585
-> 1586         self.error(obj, value)
   1587
   1588     def info(self):

~/anaconda3/envs/mpl-testing/lib/python3.6/site-packages/traitlets/traitlets.py in error(self, obj, value)
   1522                 % (self.name, self.info(), msg)
   1523
-> 1524         raise TraitError(e)
   1525
   1526

TraitError: The 'xorig' trait of a Line2D instance must be a subclass of 'numpy.core.numeric.asarray' or None, but a value of class 'list' (i.e. [0, 1, 2, 3]) was specified.

~~~
I only wanted to share this error with the blog to show that I feel as if the error is setting the data properly

I feel in order for this to work, I have to move all of the setting data aspects of `Line2D` inside of the `__init__` function
~~~
from matplotlib._traits.lines import Line2D
line = Line2D(xdata=[0,1,2,3],ydata=[0,1,2,3])
print("line", line)
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
~~~
