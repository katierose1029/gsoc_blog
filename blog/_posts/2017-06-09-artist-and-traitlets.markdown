---
layout: post
title: "Artist and Traitlets"
date: 2017-06-09
categories: jekyll update
---
Tasks for 6/9/17:
1. Look at the getters and setters in `Artist` module
2. Come up with some sort of pseudo code or strategy to converting them in terms of `Traitlets`

i.e.: How do we convert these functions in terms of transform and traitlets
~~~
def set_transform(self, t):
    """
    Set the :class:`~matplotlib.transforms.Transform` instance
    used by this artist.

    ACCEPTS: :class:`~matplotlib.transforms.Transform` instance
    """
    self._transform = t
    self._transformSet = True
    self.pchanged()
    self.stale = True

def get_transform(self):
    """
    Return the :class:`~matplotlib.transforms.Transform`
    instance used by this artist.
    """
    if self._transform is None:
        self._transform = IdentityTransform()
    elif (not isinstance(self._transform, Transform)
          and hasattr(self._transform, '_as_mpl_transform')):
        self._transform = self._transform._as_mpl_transform(self.axes)
    return self._transform
~~~

My Mentor and I had discussed:
1. `transform` default value: generates a default value for the transform attribute in `Artist`
2. `transform` validate: validate the transform attribute
3. observe `transform`: `type=change` therefore observing the change in the transform attribute

This is just a basic outline of what is to be done.

_________________________________________________________________________

Future Plans:
1. Create `Artist` directory
2. create `TraitType` for each attribute
3. `Artist(HasTraits)`

_________________________________________________________________________

Today Accomplishments:
1. created `artist` directory
2. created `tester.ipynb` for graph testing purposes
3. tested `artist.py` migration and received a plot
    * [successful is making graph after migration][gitmlp]
    * [mpl_tester.ipynb][tester]

[gitmlp]:https://github.com/katierose1029/matplotlib/commit/9b3ff6e762b23995b6dd3ad2846e4e4f0229971c
[tester]:https://github.com/katierose1029/gsoc_work/blob/master/mpl_tester.ipynb
