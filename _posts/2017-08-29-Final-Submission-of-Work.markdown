---
layout: post
title: "Final Submission of Work"
date: 2017-08-29
categories: jekyll update
---

**This following link will lead to my fork of `matplotlib`.  In this fork, I worked mainly from one branch off of the `origin/master` called `artist-traitlets-dev`.  After accomplishing one goal, I created a second branch called `line2D-traitlets-dev`.**

[https://github.com/katierose1029/matplotlib/tree/artist-traitlets-dev][https://github.com/katierose1029/matplotlib/tree/artist-traitlets-dev]

________________________________________________________________________________

**The following links lead to the pull requests I made with the following branches I created in my fork of `matplotlib`**
1. [created new branch and added `_traits` directory with artist.py and tra…][8917]
    * This was the main branch/pull request that displays the process in which I refactored `matplotlib.artist.Artist` in terms of `traitlets`
    * If you review my previous blog posts, you will see that this task was the main focus; and I was successful in completing this.
    * I was able to draw a simple figure in `matplotlib` using the refactored `Artist` module.
2. [Line2D traitlets dev][9058]
    * After completing the task of drawing a figure using the newly refactored `matplotlib._traits.artist.Artist` module, I set a goal to refactor `matplotlib.lines.Line2D`
    * This took a bit of time to understand how to refactor this module because there were many more attributes and inherited attributes involved. Not only did this module have its own process to follow, but it inherited from `matplotlib._traits.artist.Artist`

________________________________________________________________________________

**This repository was used when I was introduced to the materials/toolkits needed in order to accomplish my goals.  Also I used this repository for scrap code that I did not need at a certain moment but may have needed in the future.**

[gsoc_work][gsoc]

________________________________________________________________________________
[https://github.com/katierose1029/matplotlib/tree/artist-traitlets-dev]:https://github.com/katierose1029/matplotlib/tree/artist-traitlets-dev
[8917]:https://github.com/matplotlib/matplotlib/pull/8917
[9058]:https://github.com/matplotlib/matplotlib/pull/9058
[gsoc]: https://github.com/katierose1029/gsoc_work
