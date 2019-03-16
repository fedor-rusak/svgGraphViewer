# Interactive graph visualization with SVG (one web-page no dependencies)

[![license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

*Simple* (modern JS =>,let,const; SVG 1.1 support required) web-page that contains all necessary JS to show and interact with nodes and edges described in default graph data.

Just open [svgGraphViewer.html](svgGraphViewer.html) in your browser to see some interconnected nodes and try to move something!

## Problem

Static architecture, sequence diagrams are hard to read, modify, review. Maybe diagram with easily accessible interactivity would help to communicate the intent better.

If interactivity requires special software, subscription, access to external server than is just PITA and no one would bother with it.

So how to describe relationship, dependencies, communication between some components in some interactive way and make it easy to share?

## Proposed solution

Nothing beats web-page without dependencies as a convenient way to show and share documents. You know about internet, right?

But to make such page we would need some steps:

1. describe nodes and edges as JSON
2. chose desired visual design for visualization (typography, colors, sizes)
3. assign coordinates to nodes for visualizing aka layoting (js, basic 2d geometry)
4. visualize our JSON graph data with chosen style (JS, HTML5, SVG, DOM)
5. add some browser-event-listener that would react to clicks and moves (JS, basic 2d geometry)
6. PROFIT!

I assume you are developer or at least JSON does not scare you away. So you will modify default inputData JSON value to describe the data you need.

Visual design parts are just form of configuration on web-page i.e. variable with value *Helvetica,sans-serif*. No big deal.

Part with assigning initial node position can be a pain, but you wanted to visualize you stuff right? You definitely can start with basic multi-column approach I used.

Visualizing with DOM, SVG can be quite a pain so this part is neatly packaged inside separate stateless module with minimalistic API.

Interactivity and event listener part is sort of hard. You should track events, state, and call API for modifying visualization. But if you really want to get some fun features you can't avoid this coding part. And I got your back with some pretty good default functionality of moving whole graph and separate nodes.

## How to use

1. Copy [svgGraphViewer.html](svgGraphViewer.html) file to your local machine.
2. Modify inputData variable.
3. Reload browser to check results.
4. Modify other parts (JS, HTML, JSON) content as you wish.
5. Get back to step 3 before you are satisfied.

## Technical decisions

Custom graph data structure implementation:

 * Graph consist of nodes
 * Adding node with already existing name will be ignored
 * Each node has unique name and associated map of properties
 * Only float, boolean, strings allowed as property values
 * Any get API call returns shallow copy. Any modification to it would not change coreGraph state.
 * There is special getNodeNames and setNodeProperty API
 * Graph also contains edges
 * Each edge has unique name and associated map of properties
 * Edge adding requires valid from and to parameters, which point to existing nodes
 * Edge properties have same rules for properties as node (validation, shallow copying)
 * There is special getEdgeNames and setEdgeProperty API
 * Useful test suite to verify that most features and API work as intended

There are 2 main ways to use listeners: Set them on every object and set them on parent object of some hierarchy. I prefer second one as it gives more control over hierarchy change and desired behavior. Listeners as basis for interactivity:

* We have three main listeners: onMouseDown, onMouseMove, onMouseUp
* One is just for stability and called onMouseLeave
* Common way to make consistent behavior with listeners is to track some intermediate state
* To move whole graph I use concept of camera. If we want to move graph we move... camera operator "position"!
* With current approach you define combinedListener that works with every type of events. Be it down, move or up. And before that you define a shared state and its values. So that all the flexibility is yours.
* To interact with SVG layer I use special type-system. So that SVG elements you want to interact with should have special attributes called *name* and *type*. This allows more straight-forward code for node movement.
* Added touch support for single touch UX through touchstart, touchmove, touchend
* One is just for stability and called touchcancel

REMEMBER! IN SVG 0,0 is LEFT TOP corner! SVG as main way to render things:

* All starts from svg element that has predefined #id on a web-page
* Then we have to do something with SVG elements like g, rect, text and normal text nodes
* First we render path elements for edges. So that they are in background
* Then we render nodes so they are in foreground
* When need to move whole thing we can just set special "transform" attribute and be happy!
* Same approach for "moving" nodes. As they are rendered as elements inside special g container.
* In some cases we need width and height and for now we save it in SVG attributes
* And in case of edges we need whole bunch of info about nodes and its it attribute too!
* Render order specifies what is on top of each other. Want to move something to foreground? Rearrange svg elements order please.

## Good ideas for PR:

* Click functionality with changing colors for incoming and outgoing edges for highlighted node
* Serialization/Deserialization of graph to save/load node arrangement
* Some simple yet easy-to-grasp layout algorithm

## Bad ideas for PR:

Anyone is free to use this code as he/she desires. If someone wants to suggest PR please check this list first:

* some cool dependency like d3.js, some other external things that solves your particular issue yet is not so common for visualization of graph data for shared documents
* npm packaging, CI integrations, build scripts, browserifies, webpacks and everything else. Please use it as part of your fork.
* making svgGraphViewer module stateful? No thanks.
* adding something that would require great effor without great benefit for solving initial problem of this web-page
* support for IE6 and similair? You know it is not 2011, right?

## History

## 0.33
- docs improved
- module comments improved
- Refactoring. Module moved inside svgGraphViewer.

## 0.32
- dynamic block size calculation based on font size
- docs improved

## 0.31
- touch support
- docs improved

## 0.30
- bright border around nodes

## 0.29
- to-do ideas
- docs improved
- chosen node moved to foreground

## 0.28
- edges are moving with nodes now

## 0.27
- nodes can be moved
- root svg element now has type and name
- Refactoring. Translate as separate function now.

## 0.26
- SVG layer type system introduced. New API.
- Refactoring. Camera movement uses typed approach.

## 0.25
- bug fix for clipping svg outside initial view area

## 0.24
- experimental approach with combined listener

## 0.23
- edge geometry changed to cool bezier curves with (I hope) useful description of math behined
- slightly changed layoting start point
- added edge for default graph data

## 0.22
- dynamic width for nodes, calculated based on default font
- now x,y are actually centers of nodes
- name fix for default node fill
- improved default graph data
- improved docs

## 0.21
- whole graph can be moved

## 0.20
- mouse movement coordinates tracked when necessary
- docs improved

## 0.19
- basic listeners added

## 0.18
- edge rendering
- layouting approach improved
- data preparation step for edges

## 0.17
- layouting as a separate step
- renderGraph as high-level API
- coreGraph integrated

## 0.16
- Default graph data nodes now are rendered
- Default message now logged instead of being alerted
- Error catching for main setup steps

## 0.15
- Refactoring. Code turned into method of separate module.

## 0.14
- first rendered SVG text with 'TEXT'

## 0.13
- svgHelper introduced
- first rendered SVG rect

## 0.12
- got to SVG

## 0.11
- basic graph data structure API finished

## 0.10
- edge API imrpovement
- test improvement
- docs improved

## 0.9
- test refactoring

## 0.8
- graph data structure API added
- tests improved
- docs improved

## 0.7
- input validation added
- node names test added

## 0.6
- encapsulation improved
- graph data structure input validation test added

## 0.5
- Refactoring. Name simplification.

## 0.4
- Basic add&get node API added
- Test for encapsulation added

### 0.3
- Basis for coreGraph module with test

### 0.2
- Default graph data added

### 0.1
- Basic html file added