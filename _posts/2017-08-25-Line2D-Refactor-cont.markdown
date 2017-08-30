---
layout: post
title: "Line2D Refactor"
date: 2017-08-25
categories: jekyll update
---

Tasks for 8/25/17:
1. refactor `matplotlib.lines.Line2D`
    * look at previous notes

~~~
dashSeq = None
us_dashSeq = None
~~~
    * couldn't determien what to do with these attributes, I will keep them at None value

~~~
#code in linewidth observe
#NOTE: this line may cause recursion error
self.dashOffset, self.dashSeq = _scale_dashes(self.us_dashOffset, self.us_dashSeq, self.linewidth)
print("set self.dashOffset: ", self.dashOffset)
print("set self.dashSeq: ", self.dashSeq)
~~~
    * from set_linewidth

~~~
#dash_joinstyle validate
@validate("dash_joinstyle")
def _dash_joinstyle_validate(self, proposal):
    print("dash_joinstyle: cross validating %r" % proposal.value)
    if proposal.value is None:
        return rcParams['lines.dash_joinstyle']
    proposal.value = proposal.value.lower() #not sure on this line
    #NOTE: validJoin = ('miter', 'round', 'bevel')
    if proposal.value not in self.validJoin:
        raise ValueError('dash_joinstyle validate passed "%s";\n' % (proposal.value,)
                         + 'valid joinstyles are %s' % (self.validJoin,))
    # s = s.lower()
    # if s not in self.validJoin:
        # raise ValueError('set_dash_joinstyle passed "%s";\n' % (s,)
                        #  + 'valid joinstyles are %s' % (self.validJoin,))
    # if self._dashjoinstyle != s:
        # self.stale = True
    # self._dashjoinstyle = s
    return proposal.value
~~~
    * from set_dash_joinstyle and refactored in terms of validate

~~~
#solid_joinstyle validate
@validate("solid_joinstyle")
def _solid_joinstyle_validate(self, proposal):
    print("solid_joinstyle: cross validating %r" % proposal.value)
    if proposal.value is None:
        return rcParams['lines.solid_joinstyle']
    proposal.value = proposal.value.lower() #not sure on this line
    #NOTE: validJoin = ('miter', 'round', 'bevel')
    if proposal.value not in self.validJoin:
        raise ValueError('solid_joinstyle validate passed "%s";\n' % (proposal.value,)
                 + 'valid joinstyles are %s' % (self.validJoin,))
    # s = s.lower()
    # if s not in self.validJoin:
        # raise ValueError('set_solid_joinstyle passed "%s";\n' % (s,)
                        #  + 'valid joinstyles are %s' % (self.validJoin,))
    # if self._solidjoinstyle != s:
        # self.stale = True
    # self._solidjoinstyle = s
    return proposal.value
~~~
    * from set_solid_joinstyle

**set_markevery is giving me confusion on how to accomplish it**


**NOTE: I will start testing from here**

*Monkey Patching*
~~~

#for monkey patching into base lines
import matplotlib.lines.Line2D as b_Line2D
print('matplotlib.lines.Line2D', b_Line2D)

#for monkey patching
print('before b_Line2D.Line2D: ', b_Line2D.Line2D) #matplotlib.artist.Artist
#monkey patching
b_Line2D.Line2D = Line2D
print('after b_Line2D.Line2D: ', b_Line2D.Line2D) #matplotlib._traits.artist.Artist

~~~

**LINES OF CODE FOR TESTING**
~~~
import matplotlib
  ...: from matplotlib._traits.artist import Artist
  ...: from matplotlub._traits.lines import Line2D
  ...: import numpy as np
  ...: import matplotlib.pyplot as plt
  ...: import matplotlib.artist as baseArtist
  ...: a = baseArtist.Artist()
  ...: isinstance(a, matplotlib._traits.artist.Artist)
  ...: plt.plot([4, 3, 2, 1])
  ...: plt.ylabel('some numbers')
  ...: plt.show()
~~~
