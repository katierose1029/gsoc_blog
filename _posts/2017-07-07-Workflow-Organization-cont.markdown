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
1. List of attributes: 	
~~~
_stale = True
    Boolean

stale_callback = None
    Note: self.stale_callback(self,val)

_axes = None
    'matplotlib.axes.Axes'

figure = None
    'matplotlib.figure.Figure'

_transform = None
    'matplotlib.transforms.Transform'

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

_clippath = None
    accepts either 'matplotlib.patches.Patch' 'matplotlib.path.Path' 'matplotlib.transforms.Transform'

_clipon = True
    Boolean

_label = ''
    accepts string or anything printable with '%s' conversion
    Unicode

_picker = None
_contains = None
_rasterized = None
_agg_filter = None
_mouseover = False
eventson = False
_oid = 0
    Int
    Observer Id
_proboservers = {}
    Dict
    a dict from oids to funcs
_url = None
_gid = None
_snap = None
_sketch = ?
_path_effects = ?
_sticky edges = _XYPair([], [])
    Question -> Do I make trait?
~~~

2. Determine which attributes can be represented by traitlets already implemented
    * Is it mandatory to implement some attributes as their own trait types

3.
