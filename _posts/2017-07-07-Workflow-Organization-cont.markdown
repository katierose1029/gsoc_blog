---
layout: post
title: "Workflow Organization cont."
date: 2017-07-07
categories: jekyll update
---

Tasks for 7/07/17:
1. Understand Github project management better
2. Create breakdown of small steps for success

Accomplishing this task will allow for testing/debugging/contributing to
Matplotlib a lot more understandable & organized


Project Development Steps:
* List of attributes: 	

~~~
_stale = True
    Boolean

stale_callback = None
    Note: self.stale_callback(self,val)

_axes = None
    'matplotlib.axes.Axes'
    Instance

figure = None
    'matplotlib.figure.Figure'
    Instance

_transform = None
    'matplotlib.transforms.Transform'
    Instance

_transformSet = False
    Boolean

_visible = True
    Boolean

_animated = False
    Boolean

_alpha = None
    Float [0.0, 1.0] {transparent, opaque}

clipbox = None
    accepts a 'matplotlib.transforms.Bbox' instance
    Instance

_clippath = None
    accepts either 'matplotlib.patches.Patch' 'matplotlib.path.Path' 'matplotlib.transforms.Transform'

_clipon = True
    Boolean

_label = ''
    accepts string or anything printable with '%s' conversion
    Unicode

_picker = None
    Note sure what to do?

_contains = None
    accepts a callable function

_rasterized = None
    ACCEPTS: [True | False | None]

_agg_filter = None
    set agg_filter function

_mouseover = False
    Boolean

eventson = False
    Boolean

_oid = 0
    Int
    Observer Id

_proboservers = {}
    Dict
    a dict from oids to funcs

_url = None
    url string
    Unicode

_gid = None
    the (group) id string for the artist
    Unicode

_snap = None
    ACCEPTS: [True | False | None]

_sketch = rcParams['path.sketch']
    3 - Tuple: (scale : float, optional, length : float, optional, randomness : float, optional)

_path_effects = rcParams['path.effects']
    List of instances of matplotlib.patheffect._Base class or its derivatives

_sticky_edges = _XYPair([], [])
    Question -> Do I make trait?
    This attribute cannot be assigned to; however, the `x` and `y` lists can be modified in place as needed.
    artist.sticky_edges.x[:] = (xmin, xmax)
    artist.sticky_edges.y[:] = (ymin, ymax)
~~~

* Determine which attributes can be represented by traitlets already implemented
    * Is it mandatory to implement some attributes as their own trait types

* List of attributes that can be represented as traits from traitlets; no new TraitTypes need to be created

~~~
_stale -> Boolean
_axes -> Instance
figure -> Instance
_transform -> Instance
_transformSet -> Boolean
_visible -> Boolean
_animated -> Boolean
_alpha -> Float
clipbox -> Instance
_clipon -> Boolean
_label -> Unicode
_mouseover -> Boolean
eventson -> Boolean
_oid -> Int
_proboservers -> Dict
_url -> Unicode
_gid -> Unicode
_sketch -> Tuple
~~~

* List of attributes that either should be their own traits or I am not sure how to go about making traits of them

~~~
stale_callback -> Callable Trait type
_clippath ->
_picker -> Union Trait
    Union(Float, Boolean, Callable, default_value = None, allow_none = True)
_contains -> could be a list ?
_rasterized ->
_agg_filter ->
_snap -> Boolean(allow_none = True)
    snap = Perishable(Boolean(allow_none = True, default_value = None))
_path_effects ->
_sticky_edges ->
~~~

Git Stuff:
[Practice Git Repo][pgr]
1. rebase from command line
2. merge tool
    * current state of parent & child branch
    * combined state before they diverge
    * state which you want the branch to be in

    * visual interface for looking at those states and determining which I want the current state to be

[pgr]:https://github.com/katierose1029/testing
