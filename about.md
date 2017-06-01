---
layout: page
title: About
permalink: /about/
---

This is the base Jekyll theme. You can find out more info about customizing your Jekyll theme, as well as basic Jekyll usage documentation at [jekyllrb.com](https://jekyllrb.com/)

You can find the source code for the Jekyll new theme at:
{% include icon-github.html username="jekyll" %} /
[minima](https://jekyll.github.io/minima/)


## Contents
    1. Opening Details
        * Contact Information
        * Brief Introduction
        * Research Experience & Programming Skills
    2. Project Details
        * Abstract
        * Technical Details
        * Future Works
    3. Schedule of Deliverables
        * Community Bonding Period & Phase 1
        * Phase 2
        * Phase 3
    4. Why This Project?
    5. Appendix

## Opening Details

#### Contact Information:
* Personal Email: katiec1029@gmail.com
* School Email: kchait000@citymail.cuny.edu
* [Personal Github](https://github.com/katierose1029)
* Cell Phone: (718) 594 4909

### Brief Introduction:
My name is Kaitlyn Chait and I am a Computer Science student at The City
University of New York at The City College of New York.  When I was 15,
the high school I attended thought it was a great suggestion for me to take
my first computer science course, and I can most definitely say they were
correct.  In my opinion, the field of computer science is appealing in its
various challenges and satisfying success.  There is always a new challenge
to encounter and infinite possibilities to have success in solving the problem.

During my free time, I enjoy thrilling sports such as skiing, listening
to various genres of music and attending live music concerts.  

### Research Experience & Programming Skills:
I have been working with my mentor Dr.Michael Grossberg at the City College
of New York.  He was the one that came to me with original idea to comprise
a demonstration of a Virtual Reality application of Science on a Sphere.
Science on a Sphere is an education tool developed by the National
Oceanic Atmospheric Administration to help illustrate climate change,
changes in ocean temperature, and other weather pattens of the sorts.
After the success of our first demonstration, we wanted to expand it to
plotting live data in Jupyter notebooks and other scripts alike.

* Programming Skills:
    * Backend: Python, Java
    * Databases: MYSQL
    * Frontend: Javascript, HTML

________________________________________________________________________________

## Project Details

### Abstract
Serialization is the process in which a data structure or object is translated
and stored in the format of a file compatible in memory then reconstructed
in another environment.

The following link will bring you to a Matplotlib Enhancement Proposal
concerning the serialization of Matplotlib figures and widgets.  
[MEP25: Serialization](https://github.com/matplotlib/matplotlib/wiki/MEP25#id7)

Jupyter Notebook allow coders to compute data in an web - based interactive
environment.  Ipywidgets is a module that extends Jupyter Notebooks and
Ipython Kernel in that a coder has the ability to create interactive
HTML - based widgets.  PythreeJS is an extension of Ipywidgets, as it is a
bridge between Python widget creation and HTML widgets with the incorporation
of the Javascript 3-D graphics library, ThreeJS.

**What if we had the ability to serialize data from matplotlib figures to json
objects then render the data in a PythreeJS widget?**

### Technical Details
The following libraries/toolkits will be required throughout this project:
* **Matplotlib**
* **Ipywidgets**
* **PythreeJS**
* **jupyter-matplotlib**
* **Jupyter Notebook**
* **json**
* **BackboneJS**
* **RequireJS**
* **ThreeJS**

**Matplotlib** is a widely used plotting API amongst the coders that use
Python.  I want to implement a method that would allow plots, and other
figures alike, to serialize naturally to a format in which would be able to
be used in other widgets.

**Ipywidgets** is coded using the architectural pattern, *Model-View-Controller*.
Components of a Model-View-Controller application:
* *Model*: describes the manipulation/storage of the data and the user input
* *View*: output representation of the data; displays the data that has been
        manipulated and stored
* *Controller*: controls how the user inputs are controlled between model
        and view
![MVC Diagram](https://i.stack.imgur.com/ocEWx.png)
[src: https://i.stack.imgur.com/ocEWx.png]((https://i.stack.imgur.com/ocEWx.png))

There are a variety of widgets already programmed into Ipywidgets, however
coders can extend this library to create their own custom widgets.  The
following diagram displays how the Ipython Kernel (Backend) interacts with
the HTML widget (Frontend):
![Ipywidget Diagram](http://ipywidgets.readthedocs.io/en/latest/_images/WidgetModelView.png)
[src: http://ipywidgets.readthedocs.io/en/latest/_images/WidgetModelView.png](http://ipywidgets.readthedocs.io/en/latest/_images/WidgetModelView.png)

What the diagram does not show you is that Ipywidgets relies heavily on the
Javascript library **BackboneJS**.  **BackboneJS** is a library that gives coders
control of the structure between how models and their corresponding views
interact. In Ipywidgets, widgets are created in the backend and automatically
synchronized with their corresponding BackboneJS views in the frontend,
the widget that is seen in the notebook.

Within the code block below, you will see the source code to a small
widget called Hello and will display the test 'Hello World!'.
The first half of the code block contains the backend model of the widget
in Python and the second half contains the frontend view in Javascript.
You can see that the model is an extension of the class
*ipywidgets.widgets.DOMWidget*, which is a type of widget that directly
manipulates the DOM of the HTML widget.  Where I have the source code for
the view of the widget in Javascript, the first line of code uses
the Javascript library **RequireJS**, which is required to load the correct
modules.  The view extends the class *widgets.DOMWidgetView*, which is the
Javascript class that is overridden for the purpose of widget Hello.

1. Python (Backend Model)
~~~
import ipywidgets as widgets
from traitlets import Unicode, validate

class HelloWidget(widgets.DOMWidget):
    _view_name = Unicode('HelloView').tag(sync=True)
    _view_module = Unicode('hello').tag(sync=True)
~~~
[src](https://ipywidgets.readthedocs.io/en/latest/examples/Widget%20Custom.html#Define-the-view)

2. Javascript (Frontend View)
~~~
require.undef('hello');

define('hello', ["jupyter-js-widgets"], function(widgets) {

    var HelloView = widgets.DOMWidgetView.extend({

        // Render the view.
        render: function() {
            this.el.textContent = 'Hello World!';
        },
    });

    return {
        HelloView: HelloView
    };
});
~~~
[src](https://ipywidgets.readthedocs.io/en/latest/examples/Widget%20Custom.html#Render-method)

**ThreeJS** is a Javascript 3-D graphics library that can used to code infinite
3-D illustrations and environments.
**PythreeJS** is a bridge between Python and ThreeJS using Ipywidgets
infrastructure.  A coder can use this library to create infinite variations of
illustrations, and we will be using this *MVC* based module to view our
serialized data.

### Implementation:
The implementation of this application will be based off the
*Model-View-Controller* pattern as described before.

    *Controller*: In the following prototypes below, an object called
    Controller being used.  The design purpose of this object is to serve as
    a data controller. The two following actions are mandatory:
        * import data from a serialized representation
        * export data to a serialized representation
    This object must be implemented with a way to properly unpack/pack
    data from/to a json object file.

Note:
    * The set of data can be list, ndarray, or other representation compatible
    with Matplotlib.  When exporting data, my first focus will be *to_json*
    function, in the future I would like to work out to other data types.
    * Keep in mind unserializable aspects of a figure: how to deal with it?

In the implementation, the controller will be key, but then we will have to
deal with the serialization in PythreeJS.

### Prototype:
Here are some examples of how the serializer should work and be implemented
in a PythreeJS widget

1. Display Matplotlib figure from serialized representation:
~~~
import json
from matplotlib.controllers import Controller
with open('my_figure') as f:
    o = json.load(f)
c = Controller(o)
fig = c.figure
~~~

2. Export Matplotlib figure to json:
~~~
o = c.to_json()
# or... we should be able to throw a figure object in there too
o = Controller.to_json(mpl_fig)
~~~
[src](https://github.com/matplotlib/matplotlib/wiki/MEP25#examples)

3. Render serialized data into a PythreeJS widget:
~~~
#Import Statements
import pythreejs as py3
from ipywidgets import HTML, Text, Controller
from traitlets import link, dlink
from traitlets.traitlets import _validate_link

import json
from matplotlib.controllers import Controller
with open('my_figure') as f:
    o = json.load(f)
c = Controller(o)

#Let's say for this example we have spherical data
#We would need a variable texture that would properly
#'encompass' a sphereical object.

sphereGeometry = py3.SphereGeometry(radius = 1)
sphereMaterial = py3.BasicMaterial(map = texture)
sphere = py3.Mesh(geometry = sphereGeometry, material = sphereMaterial)

camera = py3.PerspectiveCamera(position=[2,0,2])
scene = py3.Scene(children=[])
orbit_controls = py3.OrbitControls(controlling=c)
renderer = py3.Renderer(renderer_type='webgl',camera=c, scene= s,
                            background='black', controls=[orbit_controls])
return display(renderer)
~~~

Note: The output of 3 would_be a PythreeJS Widget containing the figure.
The following image is a sample sphere I made using PythreeJS.

![PythreeJS_Sphere_Image](https://katierose1029.github.io/gsoc/PythreeJS_Sphere_Image.png)


________________________________________________________________________________

## Schedule of Deliverables

**Community Bonding Period:** (May 1st - May 28th)

**Phase 1:** (May 29th - June 23rd)
    *The focus of this stage will be Matplotlib serialization and
    how can accomplish it.*
    During this stage, I will focus on the strategy and approach to take in
    serializing a figure to json (or other format)?

**Phase 2 & Phase 3:**** (June 26th - August 25th)
    *The focus of this stage will be implementing a method in which we can
    serialize matplotlib figures*
    By this stage, I would like to start the implementation of serializing
    a Matplotlib figure. This stage will take up the bulk of the project
    due to its importance in the project. Of all the tasks to be completed
    by the end of this program, I would like this one to be completed.

**Future Work**
    After this project is complete, I would like to touch upon this in my
    future works:
    Can we alter the data in a PythreeJS widget and serialize it to a
    json?

**Hand in Final Works** (August 28th - August 29th)

________________________________________________________________________________

## Why This Project?
Completing this project would be a great addition to matplotlib and to my
portfolio as a coder.  I have some experience working with Ipywidgets, and
would like to expand upon the range in which they can be used amongst other
coders and developers.
________________________________________________________________________________

## Appendix

The following links below will give further information on the following
tools, toolkits, libraries and other modules I have mentioned throughout
this proposal.

* [BackboneJS](http://backbonejs.org/)
* [Google Cardboard](https://vr.google.com/cardboard/)
* [ipywidgets Github](https://github.com/jupyter-widgets/ipywidgets)
* [ipywidgets Documentation](https://ipywidgets.readthedocs.io/en/latest/index.html)
* [ipywidgets.widgets.DOMWidget](https://github.com/jupyter-widgets/ipywidgets/blob/master/ipywidgets/widgets/domwidget.py)
* [ipywidgets/jupyter-js-widgets](https://github.com/jupyter-widgets/ipywidgets/tree/master/jupyter-js-widgets)
* [Jupyter Notebook](https://github.com/jupyter/notebook)
* [Matplotlib](http://matplotlib.org/)
* [Oculus Rift](https://www.oculus.com/rift/)
* [pythreejs Github](https://github.com/jovyan/pythreejs)
* [RequireJS](http://requirejs.org/)
* [Science on a Sphere](https://sos.noaa.gov/What_is_SOS/)
* [ThreeJS](https://threejs.org/)

________________________________________________________________________________

You can find the source code for Jekyll at
{% include icon-github.html username="jekyll" %} /
[jekyll](https://github.com/jekyll/jekyll)
