---
layout: post
title: "TransformedPath Trait cont."
date: 2017-11-06
categories: jekyll update
---

Tasks for 11/06/17:
1. debugging `matplotlib.lines.Line2D`
    * look at notes from last posts
2. Create a `TransformedPathTrait` to be used as `transformed_path` attribute in `Line2D`

~~~
#from _traits.traits.py

class TransformedPathTrait(TraitType):
    default_value = None
    allow_none = False
    info_text = 'matplotlib.transforms.TransformedPath'
    def validate(self, obj, value):
        if value is None:
            return None #TODO: handle this
        if isinstance(value, TransformedPath):
            return value

~~~


~~~
#from _traits.lines.py

#line

~~~
