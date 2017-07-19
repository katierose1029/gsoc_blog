---
layout: post
title: "Artist with Traits cont."
date: 2017-07-18
categories: jekyll update
---

Tasks for 7/18/17:
1. Continue Artist with Traits
    * determine which functions can be brought over from original artist class.
        * ie: we will not need the get and set methods due to the migration to traitlets, however we may need some of the auxiliary functions for drawing/rendering purposes
    * Start looking into implementing ArtistInspector
2. Configure development branch origin/artist-dev with upstream/traitlets branch
    * fix pull request to upstream/traitlets
3. Discuss with mentor on how to go about testing


Notes from Call with Ryan:
* artist_withTraits.py -> artist.py
* commit from merging syntax from git caused failed
* rip out traits file and *_traits* directory
* branch off master
    * *_traits* directory
* close pull req open
    * create new pull req with cleaned up directory
* in traitlets in order to handle None
    * specify allow_none = True
* transform trait
    * return an IdenityTransform() and to work around that is to alter the set logic in traitlets
    * if i get value none i get IDTransform instead of None
* for validators and traits feel logic being implemented
    * if artist has specific logic
    * crossvalidators: purpose is to check value and cross validate between other other objects
* nit pick: no space between x = True instead do x=True keyword arguments
* underscores to be gone becuse we want coder access to these 'attributes'
* return "transform" in *self._traits_values*
    * later on self.has_trait_value("transform")
    * transform_set will be deprecated
* realtively backwards artist class
    * merge in to master
* leverage *test.py*
* implement two and three traits to run through & refactor them
    * transform or such ie.
    * run through init and run through test sweep
* class Artist(HasTraits, artist.Artist):
    * multiple inheritance
