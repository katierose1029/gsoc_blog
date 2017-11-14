---
layout: post
title: "Debugging"
date: 2017-11-14
categories: jekyll update
---

Tasks for 11/14/17:
1. debugging `matplotlib.lines.Line2D`
    * look at notes from last posts
2. Determine why we are getting a `None` error for colors

#### Progress Report For Professor
Considering I am not feeling well, I am handing in the following report:
This week I would like to discuss what has been accomplished and what is still
in progress.



In debugging the class `matplotlib._traits.lines.Line2D` I have run into a lot
of errors pertaining to the value `None`.  I have attempted to create different
traits in the `_traits.traits.py` script that handle the value of `None` in a
more controlled fashion.  However this did not end up working as well as
expected.

This caused me to come up with a different method to figure out how the values
of each attribute were being handled.  I decided to research the default values
of each attribute presented in `matplotlib.lines.lines.Line2D`
.  I forced each
of the values I found throughout my research.  For example in the code block
below, I will show lines of code before and after research.:

~~~
#Before research
color=Unicode(allow_none=True, default_value=rcParams['lines.color'])
#After research
color=Union([Unicode(), Float(), Tuple()], allow_none=False, default_value='C0')

#When the value of a trait is changed, we validate the value
@validate("color")
def _color_validate(self, proposal):
    if proposal.value is None:
        return 'C0'
    return proposal.value #we are assuming a valid value for color has been set
~~~

There are other instances throughout my code that replicate the process above.
While I was going about this process, I realized that by forcing the default
values I was finding, there was no need to create separate traits in the
`_traits.traits.py` script as I had previously hypothesized.  I thought that it
was essential to create separate traits for attributes such as `path` and
`transformed_path` because it was mandatory when coding `_traits.artist.py`
when dealing with the `transform` attribute.

Also to try and prevent further any possible `None` value errors, I set the
value of each traits `allow_none` from `True` to `False`.  
This is heavily displayed in the commit linked below:

[debugging line 2-d and trying to fix errors][commitline2d]

Currently, I am tackling and error that pertains to how the value of colors is
being handled from `Line2D` to the `matplotlib.colors.py` process.  In the code
block above, you see that `color` is set as a `Union` trait.  This is because
a color can be either a `Unicode` value (string), `Float` value, or `Tuple`
value.  This information is given to us in the documentation for the
`matplotlib.colors.py` documentation:

[colors.py][colors]

To show some of my work, here is the commit I pushed while writing this report:

[debugging facecolor/color issues][commitdebuggingfacecolor]

I apologize for not being able to make it to the meeting this week, but I hope
this written report will answer the question: What did I accomplish this week?



[commitline2d]:https://github.com/katierose1029/matplotlib/commit/c86a58fa05ca040a8bed35197462f1e1a03e0aed
[colors]:https://github.com/katierose1029/matplotlib/blob/master/lib/matplotlib/colors.py
[commitdebuggingfacecolor]:https://github.com/katierose1029/matplotlib/commit/a864143d18f9e531acced638054e180a92e35962
