# Kawasaki's Theorem

## vocabulary

### JUNCTION

a portion of the planar graph that contains

* a node (called the *origin*)
* adjacent edges
* the nodes at their endpoints
* interior angles between each edge


## implementing Kawasaki's theorem in code

to perform it locally on one **junction**:

* gather an alternate angle sums: [sum1, sum2]
  * calculate each interior angle between edges
* if [180, 180], kawasaki is proved. done.
* when values are different proceed as such:

### example

[170,190] the difference is 20 degrees. There is a causal relationship here: if just 1 angle in the first set increases by 10, it automatically shrinks the second set, so both sums are 180.

if you group each angle into groups

> A, B

any change can be made to the angles such that 

> total changes to all angles in A is +10

this can be guaranteed because when an angle changes, it affects the angles on both sides of it, by definition, angles from the opposite group. by changing A it causes

> change to B is -10

# data structure

so a data structure can be built which pairs each interior angle with the change necessary to satisfy kawasaki's theorem if only 1 angle made the change.

## application of the data structure:

to make a **junction** satisfy Kawasaki's theorem the value of the interior angles must change. To change the interior angle the endpoints associated with the edges must shift locations, while the origin node remains fixed. The simplest visualization is to imagine the edges have a fixed length and spin around the origin node.

### 1 angle is changed

simply apply the angle difference to one angle, the cause is:

* one neighbor angle (B) assumes the difference
  * change to angle A is +n
  * change to angle B is -n
* both neighboring angles (B, C) on either side change equally 
  * change to angle A is +n
  * change to angle B is -1/2 n
  * change to angle B is -1/2 n
* both neighboring angles (B, C) change uniquely
  * change to angle A is +n
  * change to angle B is -p*n
  * change to angle B is -q*n

where p+q = 1.0

### 2 or more angles changed on the same side

same as above with the quantity of change dispersed across multiple angles. the sum of changes to all angles must equal the quantity.

### 2 angles changed, one on each side

let's return to the example above: [170,190] the difference is 20 degrees

One angle must change by half of the difference. 


### all angles inherit change evenly

