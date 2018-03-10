
# Origami Voronoi

Robby Kraft

> Abstract: This paper describes a class of origami crease patterns made from Voronoi diagrams. This approach incorporates gussets between the Voronoi cells which when collapsed extend upwards and lie orthogonal to the Voronoi plane. This paper focuses on the different forms the gusset intersections can take, including the most complex case when gusset joints lie on top of one another.


## 1 Introduction

This paper will describe a class of origami made from Voronoi diagrams designed using gussets of varying thickness. Many artists have explored origami from Voronoi diagrams built with gussets of constant width (Mitani, Gjerde), and Voronoi is currently an active tool in computational origami (Tachi and Demaine, "Origamizer"). A unique quality of the approach described in this paper is the voronoi graph is preserved

### 1.1 Vocabulary

**sites**: the points from which the Voronoi diagram is originally built.

**cells**: the polygons formed by the Voronoi diagram. There is 1 cell for every site.

**gusset**: the channel inserted between 2 cells running parallel to the cell edges.

**gusset joints**: gussets intersections create details that form either a triangle or a quadrilateral.

### 1.2 Properties of each element

It’s equally approachable to imagine the gussets as paper grafted between each of the cells, as it is to imagine the cells shrinking proportionally to reveal the gussets. The width of every gusset is expressed as a magnitude of the distance between the two sites which formed the original Voronoi boundary. In the second imagination, the “shrink” is an affine scale with the homothetic center at the cell’s site. The final collapsed origami and the original voronoi lines are affine scales. Gusset joints, the intersection between 3 gussets, fall into 2 categories wether the 3 incident sites form the vertices of an acute triangle (easier) or an obtuse triangle (more complex). It’s also possible for gusset joints to overlap, which will change the crease pattern for the overlapped joint.

## 2 Folding a Voronoi diagram by hand

Under certain conditions, it’s possible to fold this Voronoi series entirely by hand. The Voronoi diagram is an expression of Origami Axiom #2. The entire process is typically done in 3 consecutive steps:

1. fold the Voronoi diagram lines.
2. crease the edges of all the gussets.
3. crease the insides of the gusset joints.

### 2.1 Crease the Voronoi diagram lines

Origami axiom #2 is “make a crease line by bringing one point onto another point".  This step can be described as “perform origami axiom 2 on the Voronoi sites, creasing only a subsection of the entire sheet.” It’s easy to spot the intersection between 3 sites which are relatively isolated. The instruction I follow is simple: 

*Crease between the two points which are globally nearest to each other, and crease only as far as I am sure it won’t crease into other cells (it’s best to play it safe).*

I iterate slowly, repeating this step by either visiting 2 uncreased points or extending a crease line as I become more certain of its length.

### 2.2 Crease the gusset edges

Gusset widths are defined as a magnitude of the distance between cell sites. The only case I typically fold by hand is where magnitude is 0.5, a crease line made at the halfway point. This is a 2 step process that involves origami axiom #1, “crease a line that passes through 2 points”:

using 2 neighboring cell sites as points for axiom #1, make a small mark on the voronoi edge, establishing the midpoint between the 2 sites.
using axiom #2, make 2 crease lines by bringing the cell sites to this midpoint. Both of these crease lines will be the same length.

The gusset edges should be the opposite crease orientation. If the Voronoi diagram creases are valley, these should be mountain.

### 2.3 Crease the interior of the gusset joints

The corners of the 3 sites around a joint form a triangle, if the Voronoi intersection (also this triangle’s circumcenter) lies inside the triangle, meaning this triangle is acute, the case is simple. Fold the edges of the triangle and rabbit ear (is this right? rabbit ear?) crimp each of the interior triangles, creating the figure in ____. If the circumcenter lies outside the triangle, this is called a complex case, and requires discussion in the following section.

## 3 Gusset Joints

A gusset joint is defined as the space occupied by the convex hull made from the 3 corners of the incident cells and the 1 vertex of the Voronoi graph which is also the triangle’s circumcenter. If the triangle is acute, the circumcenter will lie inside it, and the resulting convex hull will be a triangle. This is the easier case. The convex hull will form a quadrilateral if the circumcenter lies outside the triangle.
