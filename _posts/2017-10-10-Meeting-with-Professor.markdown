---
layout: post
title: "Determining None cont."
date: 2017-10-10
categories: jekyll update
---

Tasks for 10/10/17:
1. Meet with Professor for weekly update
2. Create `PathTrait` to try and handle the `None` situation
3. replace default_values with `rcParams[]`
4. create `test_traits.py`
    * create instances of refactored modules & a figure that follows
5. add attribute function (professor note)
    * query attributes


~~~
    linewidth=Float(allow_none=True, default_value=rcParams['lines.linewidth'])
    linestyle=Instance('matplotlib.text.Text', allow_none=True, default_value=rcParams['lines.linestyle'])
    color=Unicode(allow_none=True, default_value=rcParams['lines.color'])
    marker=Instance('matplotlib.markers',allow_none=True, default_value=rcParams['lines.marker'])
    markersize=Float(allow_none=True,default_value=rcParams['lines.markersize'])
    markeredgewidth=Float(allow_none=True,default_value=None)
    markerfacecolor=Unicode(allow_none=True, default_value=None)
    # markerfacecolor=Unicode(allow_none=True, default_value=None)
    markerfacecoloralt=Unicode(allow_none=True, default_value=None)
    fillstyle=Unicode(allow_none=True, default_value=None)
    antialiased=Bool(default_value=rcParams['lines.antialiased'])
    # accepts: ['butt' | 'round' | 'projecting']
    dash_capstyle=Unicode(allow_none=True, default_value=rcParams['lines.dash_capstyle'])
    # accepts: ['butt' | 'round' | 'projecting']
    solid_capstyle=Unicode(allow_none=True, default_value=rcParams['lines.solid_capstyle'])
    # accepts: ['miter' | 'round' | 'bevel']
    dash_joinstyle=Unicode(allow_none=True, default_value=rcParams['lines.dash_joinstyle'])
    # accepts: ['miter' | 'round' | 'bevel']
    solid_joinstyle=Unicode(allow_none=True, default_value=rcParams['lines.solid_joinstyle'])
    pickradius=Int(allow_none=True, default_value=5)
    # accepts: ['default' | 'steps' | 'steps-pre' | 'steps-mid' | 'steps-post']
    drawstyle=Instance('matplotlib.text.Text', allow_none=True,default_value='default')
~~~

~~~
class PathTrait(TraitType):

    #TODO: assure that an instance of path is being passed.
    default_value = None
    allow_none = True
    info_text = 'matplotlib.path.Path'
    def validate(self, obj, value):
        #TODO: finish this validate so we can implement
~~~
