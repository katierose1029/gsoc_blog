---
layout: post
title: "Artist with Traits cont."
date: 2017-07-11
categories: jekyll update
---

Notes from Phone Call with Ryan and Thomas:

Does `stale` and `pchanged` order matter ?
    * not sure if thought out design
    * marking things as stale will trigger a redraw
    * do I actually need to redraw? is the question to be asked
Backward compatability
    * wrapper callback get dictionary of what happened
    * decprecating callbacks will be good move towards understanding/maintaining callbacks
Top level of the mpl package
    * artist/Traits (with underscore) for development purposes
    * subclasses with traits

Other classes to look at for serialization:
1. `axisImage`
    * `axes` do before `figure`
2. `figure`
4. `text`
5. `lines`
3. `transforms`
    * major interactions with `jupyter`
