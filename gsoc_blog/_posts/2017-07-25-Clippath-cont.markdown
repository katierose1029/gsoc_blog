---
layout: post
title: "Clippath Trait cont."
date: 2017-07-25
categories: jekyll update
---

Tasks for 7/25/17:
1. `Clippath` Trait
2. Need to think about how to go about `install_trait()` function & other classes to be
dare I say *traitlet-ized* (It's not a real word I know but it's rolls off the tongue)

Other Classes to be Implemented in `traitlets`
1. `axisImage` (where is this in MPL?)
    * `axes do` before figure
2. `matplotlib.figure.Figure`
3. `matplotlib.transforms`
    * ask which transforms should be implemented in `traitlets`
    * major interactions with `jupyter`
4. `matplotlib.text.Text`
5. `matplotlib.lines.Line2D`
    * look into other lines and ask about those

~~~
# code given to me by Thomas
# This code is the start to an install function that will install traits in matplotlib

def install_traits():
import matplotlib.lines
matplotlib.lines.Line2D  = Line2DWithTraits
~~~


After committing my attempt of `clippath` (Commits [e3d07418][commit1] & [53ef0cbf][commit2]), my mentor corrected me with the code in the following code block
~~~
clippath = Union([
        Instance(TransformedPath),
        Instance("matplotlib.patches.Patch"),
    ], allow_none=True, default_value=None)

@validate("clippath")
def _validate_clippath(self, proposal):
    value = proposal.value
    from matplotlib.patches import Patch
    if isinstance(value, Patch):
        value = TransformedPatchPath(value)
    return value

def set_clip_path(self, path, transform):
    from matplotlib.patches import Rectangle, Patch

    success = False
    if transform is None:
        if isinstance(path, Rectangle):
            self.clipbox = TransformedBbox(Bbox.unit(), path.get_transform())
            self.clippath = None
        elif isinstance(path, Patch):
            self.clippath = path
        elif isinstance(path, tuple):
            path, transform = path

    if path is None:
        self.clippath = None
    elif isinstance(path, Path):
        self.clippath = TransformedPath(path, transform)
    elif isinstance(path, TransformedPath):
        # TransformedPatchPath is a subclass of TransformedPath
        self.clippath = path

    if not success:
        print(type(path), type(transform))
        raise TypeError("Invalid arguments to set_clip_path")
~~~

[commit1]:https://github.com/matplotlib/matplotlib/pull/8917/commits/e3d07418e1d141fcb513fcd238f4b48ac9419cf8
[commit2]:https://github.com/matplotlib/matplotlib/pull/8917/commits/53ef0cbf875be2cac134c88f327bbb87c4da3a47
