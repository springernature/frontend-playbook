# Object Oriented CSS



## What is OOCSS

OOCSS or 'Object Orientated CSS' is an approach to writing css that aims to encourage reusable, maintainable and predictable css. It has spawned a number of different approaches to standardise the concept most of which adhere to the core principles of OOCSS outline below.

A CSS 'object' is a repeating visual pattern, that can be abstracted into an independent snippet of HTML, CSS, and possibly JavaScript. That object can then be reused throughout a project. The aim is to break down the css declaration into the smallest blocks possible in order to maximise their potential for reuse.

An important component of OOCSS is the process of defining repeating visual features as separate modifying 'skins' that you can apply as distinctive classes to allow visual variety regardless of the structure of the HTML. In order to do this css declarations should not rely upon any assumptions about the semantics of the HTML. Instead classes are used to define 'objects' and the components therein. The layout and display of particular object or components can then be modified by additional classes or 'skins'.


The two guiding principles of OOCSS could be defined as follows:

- Separation of structure from skin: Keep the visuality separate, so you can reuse the visual classes

- Separation  of container and content: Avoid the use of location-dependent styles and always aim to identify containers and components that can be reused.


In this regard it privileges lack of repetition in the stylesheet over increases to the size of the HTML through the addition of extra classes.
The hope is that in many cases the reduced css file size will out-weight the potential bloating of the HTML.


## Why we use OOCSS

The focus on avoiding repetition makes an OOCSS particularly well suited for managing a common visual language across a number of different websites and projects.


## Common concerns

As OOCSS is more of a philosophy than a prescriptive system the implementation will naturally diverge amongst those who have decided to make use of it.There are a number of different approaches that have build upon the principles of OOCSS in a more prescriptive way. There is some difficulty in   reconciling the more 'atomic' approaches to OOCSS with design patterns such as BEM which are based more strongly around a container/component approach.


## Find out more:
- [OOCSS Wiki](https://github.com/stubbornella/oocss/wiki)
- [Introduction to OOCSS](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/)
- [Atomic CSS](https://www.smashingmagazine.com/2013/10/challenging-css-best-practices-atomic-approach/)
- [BEMM](http://getbem.com/introduction/)
