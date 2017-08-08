---
layout: post
title: "Artist with Traits cont."
date: 2017-07-21
categories: jekyll update
---

Tasks for 7/21/17:
1. `TransformTrait`
    * return an `IdentityTransform()` and to work around that is to alter the set logic in `traitlets`
    * if I get value none I get `IdentityTransform` instead of `None`
* return `transform` in `self._traits_values`
    * later on `self.has_trait_value("transform")`
    * `transformSet` will be deprecated
    * Ask mentor question on `TransformTrait` found in `traits.py`
2. `class Artist(HasTraits, artist.Artist):`
    * multiple inheritance
3. Continue implementing traits
    * ask questions pertaining to simple logic vs. not
    * for further trait implementation
4. Phone call with Thomas:
    * ask how to go about fixing picking up `_traits` in `setup.py`
    * in development phase, ask if we can import base artist class?
        * seems as if the approach Ryan is asking of me which I didnt think was the idea of this project

Questions to ask:
* `Axes` trait: does it need to be a separate trait due to the way None is handled?
* Question the `picker`: it can be either a `[None|float|boolean|callable]` yet there is no logic like `transform` or `clippath`
    * in `traits`, does this need to be like `clippath`?
    * checking for either `none`, `float`, `boolean`, `callable`?
    * contains accepts a `callable` function
* method resolution order
