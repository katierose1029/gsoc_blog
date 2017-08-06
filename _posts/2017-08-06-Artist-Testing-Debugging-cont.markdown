---
layout: post
title: "Artist Testing/Debugging cont."
date: 2017-08-06
categories: jekyll update
---

Tasks for 8/06/17:
1. Testing Artist class with Traits using Ipython
    * fixed stale recursion error yesterday so debugging should be smooth sailing

Notes:

~~~
~/Desktop/matplotlib/lib/matplotlib/_traits/artist.py in _animated_validate(self, proposal)
    281     def _animated_validate(self, proposal):
    282         print("animated: cross validating %r" % proposal.value)
--> 283         if self._animated is not proposal.value:
    284             self.pchanged()
    285             print("called self.pchanged()")

AttributeError: 'Figure' object has no attribute '_animated'
~~~
    * fixed & caused next error

~~~
~/Desktop/matplotlib/lib/matplotlib/_traits/artist.py in _animated_validate(self, proposal)
    281     def _animated_validate(self, proposal):
    282         print("animated: cross validating %r" % proposal.value)
--> 283         if self.animated is not proposal.value:
    284             self.pchanged()
    285             print("called self.pchanged()")

... last 6 frames repeated, from the frame below ...

~/anaconda3/envs/mpl-testing/lib/python3.6/site-packages/traitlets/traitlets.py in __get__(self, obj, cls)
    554             return self
    555         else:
--> 556             return self.get(obj, cls)
    557
    558     def set(self, obj, value):

RecursionError: maximum recursion depth exceeded while calling a Python object
~~~
    * commented out lines causing problems & fixed

~~~
~/Desktop/matplotlib/lib/matplotlib/_traits/artist.py in __init__(self)
    669         self.stale = True
    670         self.stale_callback = None
--> 671         self.axes = None
    672         self.figure = None
    673         self.transform = None

AttributeError: can't set attribute
~~~
    * commented out *__init__* function

~~~
~/anaconda3/envs/mpl-testing/lib/python3.6/site-packages/traitlets/traitlets.py in __init__(self, *args, **kwargs)
    992         super_args = args
    993         super_kwargs = {}
--> 994         with self.hold_trait_notifications():
    995             for key, value in kwargs.items():
    996                 if self.has_trait(key):

AttributeError: 'Rectangle' object has no attribute 'hold_trait_notifications'
~~~
    * error I was receiving before recursion stale error
    * I think this error is being caused by the clippath

Purpose of Clippath (as said by Thomas):
* it is the path that is used to clip the artist when it is drawn; instead of being careful to truncate the data at the edges, we just render everything and then clip to the axes at draw time
* [Example 1][ex1]

[ex1]:http://matplotlib.org/examples/images_contours_and_fields/image_demo_clip_path.html?highlight=clip
