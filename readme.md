# origami fold sequence

a file format for folding instructions can make possible:

* auto-generated origami diagrams
* render an animation of a folding origami

---

one sequence object can be as simple as:

```
{
	"endpoints": [  // the endpoints of the crease
		{"x": 0.5, "y": 0.0},
		{"x": 0.5, "y": 1.0}
	]
}
```

that makes a crease line.

put many of them together in an array to make the whole fold sequence for an origami

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

### however each fold sequence entry can use more information

mountain, valley, or mark

```
{
	"orientation": "mountain"
	"endpoints": [
		{"x": 0.5, "y": 0.0},
		{"x": 0.5, "y": 1.0}
	]
}
```

for curved creases

```
{
	"curve": { // absense of this implies a straight line
		// TBD. more information to describe the curve
	}, 
	"endpoints": [
		{"x": 0.5, "y": 0.0},
		{"x": 0.5, "y": 1.0}
	]
}
```

for explaining how the crease was made. 

> "Fold the top edge to the the bottom edge"

``` javascript
"instruction": {
	"axiom": 3,
	"points": { //points required for axiom instruction
		// empty, because axiom 3 uses edges
	},
	"edges": [ // edges required for axiom instruction
		[{"x": 0.5, "y": 0.0}, {"x": 0.5, "y": 1.0}],
		[{"x": 0.0, "y": 0.5}, {"x": 1.0, "y": 0.5}]
	],
	"bounds": {  // this makes it not a full-page crease
		// the bounded x or y axis 
		"a": {"x": 0.5},  // y can be used too
		"b": {"x": 0.25}
	}
}
```

## full example

``` javascript
{
	"name": "string",
	"description": "a longer string",
	"date": 15252940,
	// more stuff here, whatever you want, no specification yet. just have a "sequence" entry
	"sequence":[
		{
			"duration": 1,  // for animation, show curves
			"curve": { // absense implies straight line
				// for curved lines, TBD more information to describe the curve
			}, 
			"endpoints": [  // the endpoints of the crease
				{"x": 0.5, "y": 0.0},
				{"x": 0.5, "y": 1.0}
			],
			"orientation": "mountain",
			"instruction": { // how the crease was made. "fold top line to the diagonal line"
				"axiom": 3,
				"points": { //points required for axiom instruction
					// empty, because axiom 3 uses edges
				},
				"edges": [ // edges required for axiom instruction
					[{"x": 0.5, "y": 0.0}, {"x": 0.5, "y": 1.0}],
					[{"x": 0.0, "y": 0.5}, {"x": 1.0, "y": 0.5}]
				],
				"bounds": {  // this makes it not a full-page crease
					// the bounded x or y axis 
					"a": {"x": 0.5, "y": "undefined"},
					"b": {"x": 0.25, "y": "undefined"}
				}
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

which folds:

![crease pattern](https://cdn.rawgit.com/robbykraft/FoldSequence/master/examples/creasepattern.svg)
