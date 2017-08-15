---
layout: post
title: "Monkey Patching Debugging "
date: 2017-08-10
categories: jekyll update
---

Tasks for 8/10/17:
1. Assure monkey patching happens before dependencies are allocated

**Mentors Notes**
* `Instance` imports at the first moment an instance of `Artist` is created
* first time an instance of `Artist` gets created should be long after we have monkey patched, and probably is caused by user interaction
* you don't import `_traits.artist` then no monkey patch occurs and the library remains unaltered
    * this was my speculation after some tests yesterday

Notes:
* trying import statements at default value instantiation
