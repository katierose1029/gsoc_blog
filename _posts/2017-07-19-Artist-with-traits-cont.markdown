---
layout: post
title: "Artist with Traits cont."
date: 2017-07-19
categories: jekyll update
---

Tasks for 7/19/17:
1. Reread notes from yesterday and start those tasks
* nit pick: no space between `x = True` instead do `x=True` keyword arguments
* `artist_withTraits.py` -> `artist.py`
* rip out `traits.py` and `_traits` directory
* branch off master
    * `_traits` directory
* close pull req open
    * create new pull req with cleaned up directory
* `TransformTrait`
    * return an `IdenityTransform()` and to work around that is to alter the set logic in `traitlets`
    * if I get value none i get `IdentityTransform` instead of `None`
* return `transform` in `self._traits_values`
    * later on `self.has_trait_value("transform")``
    * `transformSet` will be deprecated
* `class Artist(HasTraits, artist.Artist):``
    * multiple inheritance
