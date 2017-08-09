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


~~~
In [12]: isinstance(matplotlib.artist.Artist, matplotlib._traits.artist.Artist)
Out[12]: False
~~~

**Conclusion of the Day:**
* monkey patching `_traits.artist.py` is failing
    * but we know we can monkey patch via Examples created

**Monkey Patching Example with Images**
[module1.first_class.py][first]
[module2.second_class.py][second]
[execution][ex]
[first]:https://github.com/katierose1029/gsoc_work/blob/master/monkey_patching_testing/module1_first_class_py.png
[second]:https://github.com/katierose1029/gsoc_work/blob/master/monkey_patching_testing/module2_second_class_py.png
[ex]:https://github.com/katierose1029/gsoc_work/blob/master/monkey_patching_testing/monkey_patching_testing_executed.png
