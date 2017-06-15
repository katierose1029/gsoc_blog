---
layout: post
title: "Artist with Traits"
date: 2017-06-15
categories: jekyll update
---

Tasks for 6/15/17:
    1. Start Skeleton for `Artist(HasTraits)`
    2. Figure out what attributes need to be TraitType

~~~
class Artist(HasTraits):

    #Axes is a TraitType
    axes = Axes('matplotlib.axes.Axes', allow_none = True)

    #alpha is an integer that represents the visiblity of a figure
    alpha = Int()
~~~
