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

#line 34
from .traits import PathTrait, TransformedPathTrait

#lines 322-324
# transformed_path=Instance('matplotlib.transforms.TransformedPath', allow_none=True) #default_value set in default function
# TransformedPath(path, self.get_transform())
transformed_path=TransformedPathTrait(allow_none=False) #TODO: assure this works

#lines 705-713
#transformed default
@default("transformed_path")
def _transformed_path_default(self):
    from matplotlib.transforms import TransformedPath
    return TransformedPath(self.path, self.get_transform())
#transformed_path validate
@validate("transformed_path")
def _transformed_path_validate(self, proposal):
    return proposal.value
~~~

This is currently not working, but I am working on getting it to work.
The error appears to be a `None` error.

Current Error:
~~~
File "/Users/KaitlynChait/Desktop/matplotlib/lib/matplotlib/_traits/lines.py", line 945, in draw
    tpath, affine = transf_path.get_transformed_path_and_affine()
AttributeError: 'NoneType' object has no attribute 'get_transformed_path_and_affine'
~~~


Testing `isinstance()` in `_traits.lines.py`:
~~~
isinstance(path, Path): False
isinstance(path, PathTrait): True
isinstance(transformed_path, TransformedPath): False
isinstance(transformed_path, TransformedPathTrait): True
~~~
