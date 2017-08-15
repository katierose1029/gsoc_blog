---
layout: post
title: "Monkey Patching Debugging "
date: 2017-08-15
categories: jekyll update
---

Tasks for 8/15/17:
1. Assure monkey patching happens before dependencies are allocated

Notes:

~~~

# axes=Instance('matplotlib.axes.Axes', allow_none=True, default_value=None)
axes=Instance(Axes, allow_none=True, default_value=None)

...

@default("axes")
    def _axes_default(self):
        print("importing Axes here")
        from matplotlib.axes import Axes
        print("successfully imported Axes")
        print("generating default axes value")
        return None
~~~
* This was unsuccessful because the import statement was not before instantiating that there is an Axes instance
    * I uncommented out the line `axes=Instance('matplotlib.axes.Axes', allow_none=True, default_value=None)` and that seemed to have not caused an error & testing with `Figure`

**This is to see where I made changes***

~~~
~/Desktop/matplotlib/lib/matplotlib/patches.py in _set_edgecolor(self, color)
    313                 set_hatch_color = False
    314
--> 315         self._edgecolor = colors.to_rgba(color, self._alpha)
    316         if set_hatch_color:
    317             self._hatch_color = self._edgecolor

AttributeError: 'Patch' object has no attribute '_alpha'
~~~
    * in line 315 I deleted the underscore


~~~
~/Desktop/matplotlib/lib/matplotlib/patches.py in _set_facecolor(self, color)
    334         if color is None:
    335             color = mpl.rcParams['patch.facecolor']
--> 336         alpha = self._alpha if self._fill else 0
    337         self._facecolor = colors.to_rgba(color, alpha)
    338         self.stale = True

AttributeError: 'Patch' object has no attribute '_alpha'
~~~
    * in line 336 I deleted the underscore

~~~
In [1]: import matplotlib
   ...: from matplotlib._traits.artist import Artist
   ...: import numpy as np
   ...: import matplotlib.pyplot as plt
   ...: import matplotlib.artist as baseArtist
   ...: a = baseArtist.Artist()
   ...: isinstance(a, matplotlib._traits.artist.Artist)
   ...: from matplotlib.patches import Patch
   ...: p = Patch()
a:  <matplotlib.artist.Artist object at 0x10f3e1be0>
matplotlib.artist b_artist:  <module 'matplotlib.artist' from '/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/artist.py'>
before b_artist.Artist:  <class 'matplotlib.artist.Artist'>
after b_artist.Artist:  <class 'matplotlib._traits.artist.Artist'>
generating default stale value
stale: cross validating True
generating default animated value
animated: cross validating False
generating default stale_callback value
importing Axes here
successfully imported Axes
generating default axes value
importing Figure here
successfully imported Figure
generating default figure value
generating default transform value
generating default transformSet value
transformSet: cross validating False
generating default visible value
visible: cross validating True
generating default alpha value
generating default clipbox value
generating default clippath value
generating default clipon value
clipon: cross validating True
generating default label value
generating default picker value
generating default rasterized value
generating default agg_filter value
generating default mouseover value
mouseover: cross validating False
generating default eventson value
eventson: cross validating False
generating default oid (observer id) value
oid: cross validating 0
generating default propobservers value
propobservers: cross validating {}
generating default url value
generating default gid (group id) value
generating default snap value
generating default sketch value
sketch: cross validating 0.0, 0.0, 0.0
generating default path_effects value
path_effects: cross validating []
generating default sticky_edges value
sticky_edges: cross validating [], []
generating default stale value
stale: cross validating True
generating default animated value
animated: cross validating False
generating default stale_callback value
importing Axes here
successfully imported Axes
generating default axes value
importing Figure here
successfully imported Figure
generating default figure value
generating default transform value
generating default transformSet value
transformSet: cross validating False
generating default visible value
visible: cross validating True
generating default alpha value
generating default clipbox value
generating default clippath value
generating default clipon value
clipon: cross validating True
generating default label value
generating default picker value
generating default rasterized value
generating default agg_filter value
generating default mouseover value
mouseover: cross validating False
generating default eventson value
eventson: cross validating False
generating default oid (observer id) value
oid: cross validating 0
generating default propobservers value
propobservers: cross validating {}
generating default url value
generating default gid (group id) value
generating default snap value
generating default sketch value
sketch: cross validating 0.0, 0.0, 0.0
generating default path_effects value
path_effects: cross validating []
generating default sticky_edges value
sticky_edges: cross validating [], []
matplotlib.patches.Patch artist.Artist:  <class 'matplotlib._traits.artist.Artist'>
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
~~~
    * **This just happened and I am not sure if this is a good or bad thing but I will be drawing a graph from here to test**

~~~
~/Desktop/matplotlib/lib/matplotlib/figure.py in _get_axes(self)
    414
    415     def _get_axes(self):
--> 416         return self._axstack.as_list()
    417
    418     axes = property(fget=_get_axes, doc="Read-only: list of axes in Figure")

AttributeError: 'Figure' object has no attribute '_axstack'
~~~
    * in line 416 I got rid of the _
        * this did not work
    * trying to delete the _ in line 415

~~~
~/Desktop/matplotlib/lib/matplotlib/figure.py in Figure()
    416         return self.axstack.as_list()
    417
--> 418     axes = property(fget=_get_axes, doc="Read-only: list of axes in Figure")
    419
    420     def _get_dpi(self):

NameError: name '_get_axes' is not defined
~~~
    * went into line 418 and got rid of the underscore

**The last two code blocks showed errors in which I encountered and tried to debug however I ended up with the same errors I had before**

**Trying to comment out __init__ function**
~~~
In [1]: import matplotlib
   ...: from matplotlib._traits.artist import Artist
   ...: import numpy as np
   ...: import matplotlib.pyplot as plt
   ...: import matplotlib.artist as baseArtist
   ...: a = baseArtist.Artist()
   ...: isinstance(a, matplotlib._traits.artist.Artist)
a:  <matplotlib.artist.Artist object at 0x10ff10cc0>
matplotlib.artist b_artist:  <module 'matplotlib.artist' from '/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/artist.py'>
before b_artist.Artist:  <class 'matplotlib.artist.Artist'>
after b_artist.Artist:  <class 'matplotlib._traits.artist.Artist'>
stale_callback: observed a change from True to None
eventson: cross validating False
Out[1]: True
~~~

~~~
In [2]: from matplotlib.figure import Figure
   ...: f = Figure()
stale_callback: observed a change from True to None
eventson: cross validating False
stale_callback: observed a change from True to None
eventson: cross validating False
matplotlib.patches.Patch artist.Artist:  <class 'matplotlib._traits.artist.Artist'>
generating default alpha value
stale: cross validating True
generating default animated value
animated: cross validating False
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
figure: cross validating <matplotlib.figure.Figure object at 0x10a790668>
figure: observed a change from None to <matplotlib.figure.Figure object at 0x10a790668>
generating default propobservers value
propobservers: cross validating {}
called self.pchanged()
stale: cross validating True
set stale: True
stale: cross validating True
stale_callback: cross validating <function _stale_figure_callback at 0x110703f28>
stale_callback: observed a change from None to <function _stale_figure_callback at 0x110703f28>
stale: cross validating True
stale: cross validating True
generating default animated value
animated: cross validating False
stale: cross validating True
stale: cross validating True
stale: cross validating True
stale: cross validating True
~~~
    * not sure if a good thing or not yet I will be trying to draw image now

**Got a recursion error in axes**
~~~
~/Desktop/matplotlib/lib/matplotlib/_traits/artist.py in _axes_validate(self, proposal)
    232                              "supported")
    233
--> 234         self.axes = proposal.value
    235         if proposal.value is not None and proposal.value is not self:
    236             self.stale_callback = _stale_axes_callback #this line needs testing

... last 6 frames repeated, from the frame below ...
~~~
    * commented line out & no more recursion error

~~~
~/Desktop/matplotlib/lib/matplotlib/_traits/artist.py in _axes_validate(self, proposal)
    234         # self.axes = proposal.value
    235         if proposal.value is not None and proposal.value is not self:
--> 236             self.stale_callback = _stale_axes_callback #this line needs testing
    237         return proposal.value
    238     #axes observer

NameError: name '_stale_axes_callback' is not defined
~~~
    * this line did need testing after all

~~~
#from base artist class & placed in same spot as base artist class

def _stale_axes_callback(self, val):
    if self.axes:
        self.axes.stale = val
~~~
    * this worked until I ran into errors with labels

**Trying out label as a `matplotlib.text.Text` instance**
~~~
#label default
    @default("label")
    def _label_default(self):
        print("importing Text here")
        from matplotlib.text import Text
        print("successfully imported Text")
        print("generating default label value")
        return None
~~~
    * this worked

~~~
TraitError: The 'clipbox' trait of a XAxis instance must be a Bbox or None, but a value of class 'matplotlib.transforms.TransformedBbox' (i.e. TransformedBbox(Bbox([[0.0, 0.0], [1.0, 1.0]]), CompositeGenericTransform(CompositeGenericTransform(BboxTransformTo(Bbox([[0.0, 0.0], [1.0, 1.0]])), Affine2D(array([[ 1.,  0.,  0.],
       [ 0.,  1.,  0.],
       [ 0.,  0.,  1.]]))), BboxTransformTo(TransformedBbox(Bbox([[0.125, 0.10999999999999999], [0.9, 0.88]]), BboxTransformTo(TransformedBbox(Bbox([[0.0, 0.0], [6.4, 4.8]]), Affine2D(array([[ 100.,    0.,    0.],
       [   0.,  100.,    0.],
       [   0.,    0.,    1.]]))))))))) was specified.
~~~

~~~
print("setting clippbox to TransformedBbox")
# print("clippbox before setting TransformedBbox", self.clippbox)
print("Bbox.unit()", Bbox.unit())
print("path.get_transform()",path.get_transform())
transformedBbox_clipbox = TransformedBbox(Bbox.unit(), path.get_transform())
print("transformedBbox_clipbox: ", transformedBbox_clipbox)
Bbox_clipbox = Bbox(transformedBbox_clipbox)
print("Bbox_clipbox: ", Bbox_clipbox)
# self.clipbox = TransformedBbox(Bbox.unit(), path.get_transform())
self.clipbox = Bbox_clipbox
~~~
* trying this code and if this works great!
    1. *transformedBbox_clipbox:* an instance of `matplotlib.transforms.TransformedBbox`
        * this module is a child of `matplotlib.transforms.Bbox`
    2. *Bbox_clipbox:* an instance of `matplotlib.transforms.Bbox`
        * this step is to assure that `self.clipbox` takes in an instance of `matplotlib.transforms.Bbox`

`def set_clip_path(self, path, transform=None)`
    * the definition line for this function needed `transform=None`

* Now I have an issues with `sticky_edges` in that I need to find a way to name the attributes of `traitlets.Tuple`
