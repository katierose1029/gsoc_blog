---
layout: post
title: "Determining None cont."
date: 2017-10-11
categories: jekyll update
---

Tasks for 10/11/17:
1. Create `PathTrait` to try and handle the `None` situation
2. create `test_traits.py`
    * create instances of refactored modules & a figure that follows

Path Trait code so far...
~~~
class PathTrait(TraitType):

    #TODO: assure that an instance of path is being passed.
    default_value = None
    allow_none = True
    info_text = 'matplotlib.path.Path'
    def validate(self, obj, value):
        #TODO: finish this validate so we can implement
~~~
