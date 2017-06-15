---
layout: post
title: "FigureTrait"
date: 2017-06-15
categories: jekyll update
---

Tasks for 6/15/17:
    1. Work on FigureTrait
    2. Skeleton for other traits

~~~
class FigureTrait(TypeCast):

    allow_none = True
    default_value = None
    klass = matplotlib.figure.Figure

    def validate(self, obj, value):
        value = super(Figure, self).validate(obj, value)
        if value not in (getattr(obj, self.name), None):
            raise ValueError("")
        if value is not None and value is not self:
            obj.stale_callback = _stale_figure_callback
        return value
~~~
