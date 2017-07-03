---
layout: post
title: "Trait Proxy"
date: 2017-06-29
categories: jekyll update
---

Tasks for 6/29/17:
1. Read through notes sent by mentor on Trait Proxy, Property Changes & Staleness

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
