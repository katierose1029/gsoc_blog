---
layout: post
title: "Rectangle Debugging cont."
date: 2017-08-08
categories: jekyll update
---

Tasks for 8/08/17:
1. Debugging Rectangle hold_trait_notifications error

Mentors Notes (**NOT MY WORDS**):
* variable Artist and thus `Artist.__init__` comes from `_traits`
* `class Patch(Artist)` was constructed using `Artist` from the base library because `_traits` had not been monkey patched yet
    * result the variable `self` is being passed to `_traits.artist.Artist.__init__` (on 689 of `patches.py`) but is an instance of `matplotlib.artist.Artist` and therefore lacks the method `hold_trait_notifications` which causes the error
