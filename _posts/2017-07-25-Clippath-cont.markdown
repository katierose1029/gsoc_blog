---
layout: post
title: "Clippath Trait cont."
date: 2017-07-25
categories: jekyll update
---

Tasks for 7/25/17:
1. Clippath Trait
2. Need to think about how to go about *install_trait()* function & other classes to be
dare I say *traitlet-ized* (It's not a real word I know but it's rolls off the tongue)

Other Classes to be Implemented in *traitlets*
1. *axisImage* (where is this in MPL?)
    * axes do before figure
2. *matplotlib.figure.Figure*
3. *matplotlib.transforms*
    * ask which transforms should be implemented in traitlets
    * major interactions with jupyter
4. *matplotlib.text.Text*
5. *matplotlib.lines.Line2D*
    * look into other lines and ask about those

~~~
# code given to me by Thomas
# This code is the start to an install function that will install traits in matplotlib

def install_traits():
import matplotlib.lines
matplotlib.lines.Line2D  = Line2DWithTraits


~~~
