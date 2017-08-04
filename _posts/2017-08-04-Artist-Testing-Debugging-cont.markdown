---
layout: post
title: "Artist Testing/Debugging cont."
date: 2017-08-04
categories: jekyll update
---

Tasks for 8/04/17:
1. Testing Artist class with Traits using Ipython

Notes:

* Error with Axes:
~~~
In [5]: import matplotlib.pyplot as plt
---------------------------------------------------------------------------
AttributeError                            Traceback (most recent call last)
<ipython-input-5-eff513f636fd> in <module>()
----> 1 import matplotlib.pyplot as plt

~/Desktop/matplotlib/lib/matplotlib/pyplot.py in <module>()
     27 from cycler import cycler
     28 import matplotlib
---> 29 import matplotlib.colorbar
     30 from matplotlib import style
     31 from matplotlib import _pylab_helpers, interactive

~/Desktop/matplotlib/lib/matplotlib/colorbar.py in <module>()
     32 import matplotlib.artist as martist
     33 import matplotlib.cbook as cbook
---> 34 import matplotlib.collections as collections
     35 import matplotlib.colors as colors
     36 import matplotlib.contour as contour

~/Desktop/matplotlib/lib/matplotlib/collections.py in <module>()
     32 from matplotlib import _path
     33 import matplotlib.mlab as mlab
---> 34 import matplotlib.lines as mlines
     35
     36 CIRCLE_AREA_FACTOR = 1.0 / np.sqrt(np.pi)

~/Desktop/matplotlib/lib/matplotlib/lines.py in <module>()
    231
    232
--> 233 class Line2D(Artist):
    234     """
    235     A line - the line can have both a solid linestyle connecting all

~/Desktop/matplotlib/lib/matplotlib/lines.py in Line2D()
    616         return bbox
    617
--> 618     @Artist.axes.setter
    619     def axes(self, ax):
    620         # call the set method from the base-class property

AttributeError: 'Instance' object has no attribute 'setter'
~~~
    * commented out line 618 mentioned above for testing

~~~

~/Desktop/matplotlib/lib/matplotlib/offsetbox.py in OffsetBox()
    188             c.set_figure(fig)
    189
--> 190     @martist.Artist.axes.setter
    191     def axes(self, ax):
    192         # TODO deal with this better

AttributeError: 'Instance' object has no attribute 'setter'
~~~

~~~
In [5]: import matplotlib.pyplot as plt
---------------------------------------------------------------------------
RuntimeError                              Traceback (most recent call last)
<ipython-input-5-eff513f636fd> in <module>()
----> 1 import matplotlib.pyplot as plt

~/Desktop/matplotlib/lib/matplotlib/pyplot.py in <module>()
    112 ## Global ##
    113
--> 114 _backend_mod, new_figure_manager, draw_if_interactive, _show = pylab_setup()
    115
    116 _IP_REGISTERED = None

~/Desktop/matplotlib/lib/matplotlib/backends/__init__.py in pylab_setup(name)
     58     # imports. 0 means only perform absolute imports.
     59     backend_mod = __import__(backend_name, globals(), locals(),
---> 60                              [backend_name], 0)
     61
     62     # Things we pull in from all backends

~/Desktop/matplotlib/lib/matplotlib/backends/backend_macosx.py in <module>()
     17
     18 import matplotlib
---> 19 from matplotlib.backends import _macosx
     20
     21 from .backend_agg import RendererAgg, FigureCanvasAgg

RuntimeError: Python is not installed as a framework. The Mac OS X backend will not be able to function correctly if Python is not installed as a framework. See the Python documentation for more information on installing Python as a framework on Mac OS X. Please either reinstall Python as a framework, or try one of the other backends. If you are using (Ana)Conda please install python.app and replace the use of 'python' with 'pythonw'. See 'Working with Matplotlib on OSX' in the Matplotlib FAQ for more information.
~~~
    * conda install pythonw.app
        * this does not work finding another way
    * [OSX config][osx]

[osx]:https://stackoverflow.com/questions/21784641/installation-issue-with-matplotlib-python
