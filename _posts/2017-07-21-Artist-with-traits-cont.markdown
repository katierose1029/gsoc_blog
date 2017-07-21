---
layout: post
title: "Artist with Traits cont."
date: 2017-07-21
categories: jekyll update
---

Tasks for 7/21/17:
1. TransformTrait
* transform trait
    * return an IdenityTransform() and to work around that is to alter the set logic in traitlets
    * if i get value none i get IDTransform instead of None
* return "transform" in *self._traits_values*
    * later on self.has_trait_value("transform")
    * transform_set will be deprecated
2. class Artist(HasTraits, artist.Artist):
    * multiple inheritance
3. Continue implementing traits
    * ask questions pertaining to simple logic vs. not
    * for further trait implementation
