---
layout: post
title: "Anatomy of Matplotlib"
date: 2017-06-01
categories: jekyll update
---
Tasks to be Completed 06/01/2017:
* [X] Lessons from Anatomy of Matplotlib
* [ ] Read through traitlets documentation

* [Anatomy of Matplotlib](https://github.com/WeatherGod/AnatomyOfMatplotlib)
* [traitlets documentation](http://traitlets.readthedocs.io/en/stable/index.html)

Things I learned:
1. How to properly graph in Matplotlib
    * methods I was using prior were a bit pathetic
2. Artist introduction
3. load% inline magic
4. print function for python 2 & 3

Things I do not understand:
1. workings behind Artist

"The Views are the ensemble of each individual Artist, which are responsible for producing the final image based on the model. The Controller will be the Controller object managing its set of Artist objects.
The Controller must be able to export the information that it’s carrying about the figure on command, perhaps via a to_json method or similar. "
[MEP25][MEP25]

To my understanding to far the Artist is the object connecting, and dare I say 'middle-man', between backend and frontend of the IPython/Jupyter Notebook.  In order to have any success in this project, I feel as if it is mandatory to know the "ins-and-outs" of the *Artist* module.

It took me a bit longer to complete the lessons that I had expected.  During the process of completing them, I wanted to assure myself that I was understanding every step of each process I was reading about.  This may not be my first time working with the Matplotlib library, but this is my first time really taking the time to fully comprehend its capabilities.

[MEP25]: [http://matplotlib.org/devel/MEP/MEP25.html]
