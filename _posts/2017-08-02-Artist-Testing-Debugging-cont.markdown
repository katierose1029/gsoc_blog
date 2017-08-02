---
layout: post
title: "Artist Testing/Debugging cont."
date: 2017-08-02
categories: jekyll update
---

Tasks for 8/02/17:
1. Testing Artist class with Traits using Ipython

Notes:
* Hannah and myself debugged my MPL and determined that *matplotlib/lib/matplotlib/_traits/__init__.py* was causing the problem with *rcParams*
    * resumed debugging
* Callable causing problem however it is a *TraitType*: 
~~~
class Callable(TraitType):
    """A trait which is callable.

    Notes
    -----
    Classes are callable, as are instances
    with a __call__() method."""

    info_text = 'a callable'

    def validate(self, obj, value):
        if six.callable(value):
            return value
        else:
            self.error(obj, value)
~~~        
