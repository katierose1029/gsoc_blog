---
layout: post
title: "Artist and Traitlets"
date: 2017-06-09
categories: jekyll update
---

Tasks for 6/14/17:
1. Continue working on Artist.axes

~~~
class Artist(HasTraits):
    axes = Axes('matplotlib.axes.Axes', allow_none=True)
~~~

Mentor Note:
If I need a MyObject type to be validated in Instance it would be ok, for me to just go Instance(MyObject) (no string used). However, what if MyObject existed in file a.py and I was creating this Instance in b.py, furthermore, imagine that a.py imports from b.py
~~~
class MyClass(HasTraits):
    i = Instance(int)
~~~

~~~
class Axes(HasTraits):
    axes = Instance('matplotlib.axes.Axes’)
~~~
