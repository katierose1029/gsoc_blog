---
layout: post
title: "Line2D Refactor"
date: 2017-08-23
categories: jekyll update
---

Tasks for 8/23/17:
1. refactor `matplotlib.lines.Line2D`
    * look at previous notes

All Attributes:
    * Note not all of these will be used but these are from original `__init__` function

~~~
# skeleton code for decorators
# default
@default("")
def __default(self):
    print(": generating default value")
    return False
# validate
@validate("")
def __validate(self, proposal):
    print(": cross validating %r" % proposal.value)
    return proposal.value
# observer
@observe("", type="change")
def __observe(self, change):
    print(": observed a change from %r to %r" % (change.old, change.new))



# xorig = np.asarray([])
xorig = Instance('numpy.asarray', allow_none=True,default_value=[]) #not sure on this line ay have to declare default value in default decorator

# yorig = np.asarray([])
yorig = Instance('numpy.asarray', allow_none=True,default_value=[]) #not sure on this line ay have to declare default value in default decorator

# invalidx = True
invalidx=Bool(default_value=True)
# invalidy = True
invalidy=Bool(default_value=True)



# x = None
x=Instance('numpy.asarray', allow_none=True,default_value=None) # not sure on this line
# y = None
y=Instance('numpy.asarray', allow_none=True,default_value=None) # not sure on this line
# xy = None


# path = None
# transformed_path = None
# subslice = False
# x_filled = None # used in subslicing; only x is needed
# set_data(xdata, ydata)

scaled dash + offset
dashSeq = None
dashOffset = 0
unscaled dash + offset
this is needed scaling the dash pattern by linewidth
us_dashSeq = None
us_dashOffset = 0
~~~
