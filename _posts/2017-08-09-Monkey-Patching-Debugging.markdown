---
layout: post
title: "Monkey Patching Debugging "
date: 2017-08-09
categories: jekyll update
---

Tasks for 8/09/17:
1. Catching where instance of `_traits.artist.py` is being created
2. Understand where the monkey patching of `_traits.artist.py` is failing into `matplotlib.artist.py`


**Monkey Patching Example with Images (8/08/17)**
* [module1.first_class.py][first]
* [module2.second_class.py][second]
* [execution][ex]

~~~
In [1]: import matplotlib
   ...: from matplotlib._traits.artist import Artist
   ...: import numpy as np
   ...: import matplotlib.pyplot as plt
matplotlib.artist b_artist:  <module 'matplotlib.artist' from '/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/artist.py'>
b_artist.Artist:  <class 'matplotlib.artist.Artist'>
traits: b_artist.Artist:  <class 'matplotlib._traits.artist.Artist'>

In [2]: a = Artist()
generating default stale value
stale: cross validating True
generating default animated value
animated: cross validating False
generating default stale_callback value
generating default axes value
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

In [3]: isinstance(matplotlib.artist.Artist, matplotlib._traits.artist.Artist)
Out[3]: False
~~~


[first]:https://github.com/katierose1029/gsoc_work/blob/master/monkey_patching_testing/module1_first_class_py.png
[second]:https://github.com/katierose1029/gsoc_work/blob/master/monkey_patching_testing/module2_second_class_py.png
[ex]:https://github.com/katierose1029/gsoc_work/blob/master/monkey_patching_testing/monkey_patching_testing_executed.png
