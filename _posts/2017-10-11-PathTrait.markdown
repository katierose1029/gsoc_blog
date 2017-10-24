---
layout: post
title: "Determining None cont."
date: 2017-10-11
categories: jekyll update
---

Tasks for 10/11/17:
1. Create `PathTrait` to try and handle the `None` situation
2. create `test_traits.py`
    * create instances of refactored modules & a figure that follows

Path Trait code so far...
~~~
class PathTrait(TraitType):

    #TODO: assure that an instance of path is being passed.
    default_value = None
    allow_none = True
    info_text = 'matplotlib.path.Path'
    def validate(self, obj, value):
        #TODO: finish this validate so we can implement
~~~

Code to be tested:
1. `matplotlib._traits.traits`

~~~
class PathTrait(TraitType):
    #TODO: assure that an instance of path is being passed.
    # default_value = None
    default_value=Path([(0.0,0.0),(1.0,0.0),(1.0,1.0),(1.0,0.0)])
    allow_none = False
    info_text = 'matplotlib.path.Path'
    def validate(self, obj, value):
        if value is None:
            #try returning an instance of Path
            return Path([(0.0,0.0),(1.0,0.0),(1.0,1.0),(1.0,0.0)])
        if isinstance(value, Path):
            return value
~~~

2. `matplotlib._traits.lines`

~~~
path = PathTrait(allow_none=False, default_value=Path([(0.0,0.0),(1.0,0.0),(1.0,1.0),(1.0,0.0)]))

@validate("path")
def _path_validate(self, proposal):
    # print("path: cross validating %r" % proposal.value)
    return proposal.value
~~~



Testing in ipython:
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
a:  <matplotlib.artist.Artist object at 0x1091600f0>
setting the data here
called set_data(xdata, ydata)
x [0, 1, 2, 3]
y [0, 1, 2, 3]
called set_xdata
called set_ydata
successfully set the data
self.xy  None
line Line2D()
line.linewidth 1.5
line.linestyle None
line.color C0
line.marker None
line.markersize 6.0
line.markeredgewidth None
line.markerfacecolor None
line.markerfacecoloralt None
line.fillstyle None
line.antialiased True
line.dash_capstyle butt
line.solid_capstyle projecting
line.dash_joinstyle round
line.solid_joinstyle round
line.pickradius 5
line.drawstyle None
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

In [2]: from matplotlib.path import Path

In [3]: isinstance(line.path, Path)
Out[3]: True
~~~

This could have possible fixed the `path` issue but I have to fix the `xy=None` issue now.

~~~
self.drawstyle  None
self.xy  [[ 0.  0.]
 [ 0.  1.]]
~~~

After seeing these print statements, I do not think that the issue is `xy` at this point, I think it is `drawstyle`
    * changed default value of `drawstyle` to `'default'`

Alteration in `axis.py`
~~~
#lines 459-467
print("l.path at this point", l.path)
# print("l.get_path() at this point", l.get_path())
# l.get_path()._interpolation_steps = GRIDLINE_INTERPOLATION_STEPS
p = l.path
print("p ", p)
interpolation_steps = p._interpolation_steps
print("interpolation_steps ", interpolation_steps)
l.path._interpolation_steps = GRIDLINE_INTERPOLATION_STEPS
print("l.path._interpolation_steps ", l.path._interpolation_steps)

#line 592 - 601
# l.get_path()._interpolation_steps = GRIDLINE_INTERPOLATION_STEPS
print("get_gridline l.path at this point", l.path)
# print("l.get_path() at this point", l.get_path())
# l.get_path()._interpolation_steps = GRIDLINE_INTERPOLATION_STEPS
p = l.path
print("get_gridline p ", p)
interpolation_steps = p._interpolation_steps
print("get_gridline interpolation_steps ", interpolation_steps)
l.path._interpolation_steps = GRIDLINE_INTERPOLATION_STEPS
print("get_gridline l.path._interpolation_steps ", l.path._interpolation_steps)
~~~

Alteration in `axes/_base.py`
~~~
#lines 1779
# path = line.get_path()
print("line.path ", line.path)
path = line.path
~~~

**Update**: we have a figure with no line but we have a figure!

*Error*:
`TypeError: <lambda>() missing 1 required positional argument: 'y'`
* this error has been popping up in a few spots and I have an idea on how to counter it.
* *idea*: change default values for `path`...
    * this did not work as expected...
