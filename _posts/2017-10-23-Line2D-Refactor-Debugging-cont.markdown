---
layout: post
title: "Line2D Refactor & Debugging"
date: 2017-10-23
categories: jekyll update
---

Tasks for 10/23/17:
1. debugging `matplotlib.lines.Line2D`
    * look at notes from last posts

Notes to say tomorrow:
* `transformed_path` is the next `None` issue to toy with
* I think I may have a solution in that:
    - validation logic must be similar to the function `transformed_path()` but setting the value of `transformed_path` via validate.
    - like the issue with `artist.Artist.set_clip_path` function, I do not think these functions for now are codependent.  This right now is likely because of the module dependency on the `transform_path` function.
    - this codependency issue will be resolved once we resolve the issue of debugging the `None` value of `transformed_path`
    - another possible solution to this issue may be to create a `TransformedPathTrait` in `traits.py` with it's own validation logic like `transform_path`
