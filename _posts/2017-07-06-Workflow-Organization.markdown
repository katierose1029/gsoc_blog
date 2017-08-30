---
layout: post
title: "Artist with Traits Continued and Workflow Organization"
date: 2017-07-06
categories: jekyll update
---

Tasks for 7/06/17:
1. Continue implementing `Artist` using `traitlets`
2. Understand Github project management better

Note: There are some attributes in `Artist` that do not need their own
trait implemented separately. These attributes can be represented using an
`Instance` trait

Note: We are taking a step back in order to understand the workflow of github
branches so that instead of making one big pull request, we will be making small
incremental ones in order to succeed


Notes from Mentor Call:

1. create single pull req
2. create multiple pull that can be slowly merged into matplotlib
3. not just going to have one branch
    * small branches for small changes
4. create pull req in which artist becomes directory as opposed to a single file
    * on my fork of katie/matplotlib
    * my master branch should be = to mpl/master
5. do not want to make changes on upstream
6. create a branch unique on origin repo
    * make pull req into some other branch on upstream
        * in this case master
7. making series of pull req
    * allows for small incremental steps in development
8. features x y and z to add to upstream
	* changes need to occur z req y and y req x to function
    * merge x then y then z in order for upstream to be functional at all times
	* create branch for feature x
	   * create branch for feature y from feature x ... and so on
9. rebase
    * Let's say we have features x and y; x is branched off of master and y is branched from x (x is required for y)
    * Now let's say that master/x gets ahead of y we can rebase x so that the commits on y are 'on top of' the commits of x therefore not causing a merge error  
