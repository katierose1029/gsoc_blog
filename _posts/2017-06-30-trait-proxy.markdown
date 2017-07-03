---
layout: post
title: "Trait Proxy cont."
date: 2017-06-30
categories: jekyll update
---

Tasks for 6/30/17:
1. Descriptors
2. Speak with Mentor on next plan for project

_______________________________________________________________________________
#create descriptor that will set a defaut value only on
#instances of MyClass

~~~
class MyBaseClass(HasDescriptors):

  def __init__(self):
    self._data = {}


class Descriptor(BaseDescriptor):

  # add methods here

  def __init__(self, default):
  	self.default_value = default

  #obj is the instance that is being created
  def instance_init(self, obj):
    """
    if isinstance:
    	obj.data ...
    """
    if type(obj) is
    obj._data[self.name] = self.default_value

  def subclass_init(self, cls):
    obj._data[self.name] = None

  def __get__(self, obj, cls):
    return obj._data[self.name]


class MyClass(MyBaseClass):

  # put the descriptor here
	d = Descriptor("default")


c = MyClass()
c.d # returns the string "default"

class MySubclass(MyClass):
  pass

s = MySubclass()
s.d # raises an error

# - - - - - - - - - - - -

Descriptors

Classes own descriptors

Subclasses that know of descriptors

Instances that know of descriptors

~~~
