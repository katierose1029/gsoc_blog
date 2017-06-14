---
layout: post
title: "Continuing Axes Trait"
date: 2017-06-14
categories: jekyll update
---

Tasks for 6/14/17:
1. Continue working on Artist.axes

~~~
class Artist(HasTraits):
    axes = Axes('matplotlib.axes.Axes', allow_none=True)
~~~

Mentor Note: (I AM QUOTING HIM AS A MENTAL NOTE)
If I need a MyObject type to be validated in Instance it would be ok, for me to just go Instance(MyObject) (no string used). However, what if MyObject existed in file a.py and I was creating this Instance in b.py, furthermore, imagine that a.py imports from b.py
~~~
class MyClass(HasTraits):
    i = Instance(int)
~~~

You should generally be making traits when there is not a type which fully represents the value, or attributes of that type should have certain universal behaviors. For example, if matplotlib had a Color object (pretty sure they don't), then it might not be necessary to create a new trait since you could just do Instance(Color).

~~~
class Axes(HasTraits):
    axes = Instance('matplotlib.axes.Axes’)
~~~
