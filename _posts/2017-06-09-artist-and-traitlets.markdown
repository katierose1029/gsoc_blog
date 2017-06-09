---
layout: post
title: "Artist and Traitlets"
date: 2017-06-09
categories: jekyll update
---
Tasks for 6/9/17:
1. Look at the getters and setters in Artist module
2. Come up with some sort of pseudo code or strategy to converting them in terms of Traitlets

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
1. transform default value: generates a default value for the transform attribute in Artist
2. transform validate: validate the transform attribute
3. observe transform: type=change therefore observing the change in the transform attribute

This is just a basic outline of what is to be done.

_________________________________________________________________________

1. Create Artist directory
2. create trait scripts with respective classes
