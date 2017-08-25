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
