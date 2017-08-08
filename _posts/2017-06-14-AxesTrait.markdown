---
layout: post
title: "AxesTrait"
date: 2017-06-14
categories: jekyll update
---

Tasks for 6/14/17:
1. determine which classes need a new trait altogether
2. work on `Axes`

Instead of using `TraitType`, my mentor suggested I use `TypeCast`:
* type checking occurs in `TypeCast.validate`
    * builtin validation logic
    * `klass = <whatever type you want>`
    * `super(Axes, self).validate(obj, value)``

~~~
class AxesTrait(TypeCast):

    allow_none = True
    default_value = None
    klass = matplotlib.axes.Axes

    def validate(self, obj, value):
        value = super(Axes, self).validate(obj, value)
        if value not in (getattr(obj, self.name), None):
            raise ValueError("Can not reset the axes. You are "
                "probably trying to re-use an artist in more "
                "than one Axes which is not supported.")
        if value is not None and value is not self:
            obj.stale_callback = _stale_axes_callback
        return value
~~~

~~~
class Artist(HasTraits):
    axes = AxesTrait('matplotlib.axes.Axes', allow_none=True)
~~~
