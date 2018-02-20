# origami fold sequence

a file format to describe set of folding instructions

makes possible:

* auto-generated origami diagrams
* render a folding animation of the origami

---

## Overview

To represent a step by step instruction an ordered array stores each step. Each step is a fold instruction where the details of each fold are described in terms of the creases put into the material.

## Format

each step is describing the new crease line

``` javascript
{
  "endpoints": [  // the endpoints of the crease line
    {"x": 0.5, "y": 0.0},
    {"x": 0.5, "y": 1.0}
  ]
}
```

put many of these together in an array and you have the step by step instructions for an origami

``` javascript
"sequence":[
  {
    "endpoints": [
      {"x": 0.5, "y": 0.0},
      {"x": 0.5, "y": 1.0}
    ]
  },
  {
    "endpoints": [
      {"x": 0.0, "y": 0.5},
      {"x": 1.0, "y": 0.5}
    ]
  },
  // continued...
]
```

**however, each step needs more information**

mountain, valley, or mark

``` javascript
{
  "orientation": "mountain",
}
```

curved creases

``` javascript
{
  "curve": {
    bezier: {},
    parametric: {},
    // more ways to define a curve
  }, 
}
```

a record for explaining how the crease was made

> "Fold the top edge to the the bottom edge"

``` javascript
{
  "axiom": {
    "number": 3,
    "edges": [ // edges required for axiom instruction
      [{"x": 0.0, "y": 0.0}, {"x": 0.0, "y": 1.0}],
      [{"x": 1.0, "y": 0.0}, {"x": 1.0, "y": 1.0}]
    ]
  }
}
```

this is the axiom object

it has more properties too

``` javascript
"axiom": {
  "number": 3,
  "points": { // if axiom is defined by points
    // empty, because axiom 3 uses edges
  },
  "edges": [ // edges required for axiom instruction
    [{"x": 0.0, "y": 0.0}, {"x": 0.0, "y": 1.0}],
    [{"x": 1.0, "y": 0.0}, {"x": 1.0, "y": 1.0}]
  ],
  "bounds": {  // this makes it not a full-page crease
    // the bounded x or y axis 
    {"y": 0.5},
    {"y": 1.0}
  }
}
```

## Ways to define a fold

the crease needs at least 1: "endpoints", "curve", or "axiom"

``` javascript
{
  endpoints: [],
  curve: {},
  axiom: {}
}
```

the crease can be defined from only the "axiom" object, without "endpoints".

``` javascript
{
  "axiom": {
    "number": 3,
    "edges": [
      [{"x": 0.0, "y": 0.0}, {"x": 0.0, "y": 1.0}],
      [{"x": 1.0, "y": 0.0}, {"x": 1.0, "y": 1.0}]
    ]
  }
}
```

the crease can be defined by an equation

``` javascript
{
  "curve": {
    parametric:{
      // example: a sign curve, with amplitude and frequency
      // - in units relative to the page dimensions
    }
  }
}
```

there are a few ways to define a crease. to guard against redundency there is an order of importance:

1. "axiom"
2. "curve"
3. "endpoints"

or switch 1 and 2

1. "curve"
2. "axiom"
3. "endpoints"

## verbose example

``` javascript
{
  "name": "title of piece",
  "description": "description of piece",
  "date": 15252940,  // what's a good date format to use?
  // more stuff here, whatever you want, no specification yet. just have a "sequence" entry
  "sequence":[
    {
      "duration": 1,  // for animation, show curves
      "curve": { // absense implies straight line
        // for curved lines, TBD more information to describe the curve
      }, 
      "endpoints": [  // the endpoints of the crease
        {"x": 0.5, "y": 0.5},
        {"x": 1.0, "y": 1.0}
      ],
      "orientation": "mountain",  // mountain, valley, or mark
      "axiom": { // how the crease was made. "fold top line to the diagonal line"
        "number": 3,
        "points": { //points required for axiom instruction
          // empty, because axiom 3 uses edges
        },
        "edges": [ // edges required for axiom instruction
          [{"x": 0.0, "y": 0.0}, {"x": 0.0, "y": 1.0}],
          [{"x": 1.0, "y": 0.0}, {"x": 1.0, "y": 1.0}]
        ],
        "bounds": [  // this makes it not a full-page crease
          // the bounded x or y axis 
          {"y": 0.5},
          {"y": 1.0}
        ]
      }
    },
    {
      // more sequence objects follow
    }
  ]
}
```

# tiny example

``` javascript
{
  "sequence":[
    {
      "orientation": "mountain",
      "endpoints": [
        {"x": 0.5, "y": 0.0},
        {"x": 0.5, "y": 1.0}
      ]
    },
    {
      "orientation": "mountain",
      "endpoints": [
        {"x": 0.0, "y": 0.5},
        {"x": 1.0, "y": 0.5}
      ]
    },
    {
      "orientation": "valley",
      "endpoints": [
        {"x": 0.0, "y": 0.0},
        {"x": 1.0, "y": 1.0}
      ]
    },
    {
      "orientation": "valley",
      "endpoints": [
        {"x": 0.0, "y": 1.0},
        {"x": 1.0, "y": 0.0}
      ]
    }
  ]
}
```

which makes:

![crease pattern](https://cdn.rawgit.com/robbykraft/FoldSequence/master/examples/creasepattern.svg)
