# origami fold sequence

one sequence object can be as simple as

```
{
	"endpoints": [  // the endpoints of the crease
		{"x": 0.5, "y": 0.0},
		{"x": 0.5, "y": 1.0}
	]
}
```

put many of them together in an array to make the whole fold sequence for an origami piece

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

a sequence of folds like this can be used to auto-generate origami diagrams

### however each fold sequence entry needs more information

for curved creases

```
{
	"curve": { // absense of this implies a straight line
		// TBD. more information to describe the curve
	}, 
	"endpoints": [  // the endpoints of the crease
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

## example


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
		{
			"endpoints": [
				{"x": 0.0, "y": 0.0},
				{"x": 1.0, "y": 1.0}
			]
		},
		{
			"endpoints": [
				{"x": 0.0, "y": 1.0},
				{"x": 1.0, "y": 0.0}
			]
		}
	]
}
```