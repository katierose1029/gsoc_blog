---
layout: post
title: "Trait Proxy"
date: 2017-06-29
categories: jekyll update
---

Tasks for 6/29/17:
1. Read through notes sent by mentor on `TraitProxy`, Property Changes & Staleness

### Notes from Mentor:
On Property Changes and Staleness
The key problem of reconciling the concepts of "property" changes (anything handled by pchanged) and artist staleness into traitlets is one of order. While the order in which a given group of observers gets called is always the same, that ordering is arbitrary. Thus, in traitlets, all observers should assume that they have no particular arrangement.
For property changes and staleness however, order does matter. Callbacks which respond to property changes must occur before an Artist is marked as stale and redrawn, because they may in turn mark other Artists as stale and in need of being redrawn.
This conflict over order means that one cannot simply observe all property changes with a callback that marks an Artist as stale, because there may be other property dependent callbacks that will get triggered after we have marked the object as stale. To get around this we must create a Perishable trait which sets stale = True after having finished notifying observers:
To accomplish that goal we create a a ProxyTrait which simply wraps another one. We don't create a subclass for a given trait (say an Int), because we would alternatively need to create a subclass with perishable logic for all existing trait types. Thus with a ProxyTrait we can simply wrap a known trait with additional logic. In other words, TraitProxy(Int()) acts in all respects like a plain Int, but a subclass of TraitProxy could change how and when the base methods of its trait are called.


~~~
class TraitProxy(TraitType):

    def __init__(self, trait):
        self.__trait = trait

    def instance_init(self, obj):
        self.__trait.instance_init(obj)

    def class_init(self, cls, name):
        self.__trait.class_init(cls, name)

    def set(self, obj, val):
        self.__trait.set(obj, val)

    def get(self, obj, cls):
        return self.__trait.get(obj, cls)

    def __getattr__(self, name):
        return getattr(self.__trait, name)
~~~


~~~
class Perishable(TraitProxy):

    def set(self, obj, val):
        super(Perishable, self).set(obj, val)
        obj.stale = True
~~~
