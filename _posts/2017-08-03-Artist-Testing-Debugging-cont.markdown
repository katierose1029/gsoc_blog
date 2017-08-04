---
layout: post
title: "Artist Testing/Debugging cont."
date: 2017-08-03
categories: jekyll update
---

Tasks for 8/03/17:
1. Testing Artist class with Traits using Ipython

Notes:
* *picker* contained more arguments than expected
* *Any* trait had to be imported
* *default_value* of *Tuple* in *sketch* turned out to be *None*

~~~
_traits/artist.py
# sketch=Tuple(Float(),Float(),Float(), default_value=rcParams['path.sketch'])
sketch=Tuple(Float(),Float(),Float())
~~~

~~~
_traits/artist.py
#sketch default
@default("sketch")
def _sketch_default(self):
    print("generating default sketch value")
    return rcParams['path.sketch']
~~~

* *@observe("name_of_attribute", type=change)*
    * change is not being recognized
~~~
_traits/artist.py
# @observe("name_of_attribute", type=change)
@observe("name_of_attribute", type="change")
~~~

* Lines of code worked in *Ipython Terminal*:
    * [1]: *import matplotlib._traits.artist*
    * [2]: *import matplotlib._traits.traits*

* Creating an instance of Artist has allowed other errors to come up:
    * *path_effects=List(Instance('matplotlib.patheffects._Base'), default_value=rcParams['path.effects'])*
        * *_Base* is not a module
        * trying to see if by getting rid of *_Base* can I fix the problem?
