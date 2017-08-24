---
layout: post
title: "Line2D Refactor"
date: 2017-08-23
categories: jekyll update
---

Tasks for 8/23/17:
1. refactor `matplotlib.lines.Line2D`
    * look at previous notes

Notes:
~~~
# This is the first block of code I will be dealing with for the day: I know for that this belongs in linestyle but I need to test/assure myself that this belongs in the default or validate decorator. (I am thinking decorator)

# this may have to go in the linestyle validation function
if isinstance(linestyle, six.string_types):
    ds, ls = self._split_drawstyle_linestyle(linestyle)
    if ds is not None and drawstyle is not None and ds != drawstyle:
        raise ValueError("Inconsistent drawstyle ({0!r}) and "
                         "linestyle ({1!r})".format(drawstyle,
                                                    linestyle)
                         )
    linestyle = ls

    if ds is not None:
        drawstyle = ds
~~~

**This code below is to be tested**
~~~
#linestyle validate
@validate("linestyle")
def _linestyle_validate(self, proposal):
    print("linestyle: cross validating %r" % proposal.value)
    if proposal.value is None:
        return rcParams['lines.linestyle']

    if isinstance(proposal.value, six.string_types):
        # ds, ls = self._split_drawstyle_linestyle(linestyle)
        # if ds is not None and drawstyle is not None and ds != drawstyle:
        #     raise ValueError("Inconsistent drawstyle ({0!r}) and "
        #                      "linestyle ({1!r})".format(drawstyle,
        #                                                 linestyle)
        #                      )
        ds, ls = self._split_drawstyle_linestyle(proposal.value)
        if ds is not None and self.drawstyle is not None and ds != drawstyle:
            raise ValueError("Inconsistent drawstyle ({0!r}) and "
                             "linestyle ({1!r})".format(self.drawstyle,
                                                        proposal.value)
                             )
        # linestyle = ls

        if ds is not None:
            # drawstyle = ds
            self.drawstyle = ds
            return proposal.value
    # return proposal.value
~~~
