# svgGraphViewer idea

[![license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

Simple (fresh JS, SVG support required) web-page that contains all necessary JS to show and interact with nodes and edges of some default graph data.

## Instructions

Just open [svgGraphViewer.html](svgGraphViewer.html) in your browser to start application.

## Goal

Have a interactive web-page with graph-interactive functionality that can be adapted to specific case. Like add specific shapes, colors, behaviors and etc without learning new super fancy API.

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

TO-DO:

* Listeners as basis for interactivity

SVG as main way to render things (WIP):
* All starts from svg element that has predefined #id on a web-page
* Then we have to do something with SVG elements like g, rect, text and normal text nodes

## History

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