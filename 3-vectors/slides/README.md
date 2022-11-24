# Slides 3 - Vectors

## General Definition

### Mathematical

```
v = (1/2/3)
```

- A List of `n` Numbers. (i.e. `Array`)
- Where `n` describes the Dimension of the vector
- Each number of a Vector is usually assigned a letter. - The standard is: `x,y,z,w` in that order.
- Opposite: Scalar. (a single number)

### Geometrical

A vector is a directed line segment that contains:
- magnitude: the length of the vector
- direction: which way the vector is pointing

It is depicted using an Arrow.
- the tail is the start point of the vector
- the head is the pointy end of the arrow, which shows the direction

A vector has NO POSITION in a coordinate system
- it describes rather a DISPLACEMENT
  - e.g. go three steps north and one step east
- or a VELOCITY
  - e.g. a car is moving 10km/h South

- DISPLACEMENT is a Vector value.
  - distance is a Scalar value describing its magnitude.
- VELOCITY is a Vector value.
  - speed is a Scalar value describing its magnitude.

#### Sequence of Displacements

A vector like `(2/3)` describes a combination of a displacement 
- on positive x by two units
- on positive y by three units

The resulting vector is the direct line from start to end.
- basically the "shortcut" if you were to directly walk towards the final point.

## Zero Vector

A zero Vector is a Vector in which all components have the value zero: `(0/0/0)`

The zero Vector `0` fulfills the requirement:
- `v + 0 = v`

### Mathematical

Special:
- no direction
- a magnitude of zero.

### Geometrical

It is not a POINT. Consider it as "No Displacement":

## Vector != Point

Even though almost all Frameworks use the same Data Type `Vector` to describe both Displacements and Positions, they are not the same.

### A Vector Describes a Placement

e.g. 5 meter east, 2 meter north

### A Point is an absolute position

There is no example of this, since absolute positions don't really exist.

### A Point is actually a relative position

It requires a reference point, which we call `origin`, e.g.:
- GPS Coordinates have a reference point which is `0˚N,0˚E`
- Temperatures have a reference point, which is `0˚`
  - `0˚C` is the temperature at which water freezes
  - `0˚K` is the smallest measurable temperature
- Velocity has a reference point
  - When you say that you're moving 50km/h North
  - You mean that you are moving at that speed and direction
  - Compared to Earth's movement around the Sun
  - And its rotation around itself

Therefore, we come to the definition:

```
Point = Origin + Displacement
```

One more example: A Date.

- `27.01.2022` describes the amount of days that have passed since the Origin. `01.01.0000`
- `3 days` describe a displacement.

### Vectors versus Maths

They are
- mathematically identical
- conceptually distinct

### Why we use the Same Data Type

Because using separate Data Types makes both writing and reading code more difficult.

## Negating a Vector

Negating a vector returns a Vector, such that for Vector `v`, the negated vector `-v` fulfills the requirement:
- `v+(-v)=0`

### Mathematical

When negating a Vector, all of its components are negated:
- `-(x/y/z) = (-x/-y/-z)`

Examples:

- `-(3/4/5) = (-3/-4/-5)`
- `-(2/-1/0) = (-2/1/0)`

### Geometrical

Negating a vector
- flips its direction (Head and Tail are swapped)
- retains its magnitude

## Scalar Multiplication

Scalar Multiplication describes multiplying a Vector `v` with a scalar value `k`.

### Mathematical

When multiplying a vector with a scalar value `k`, all of its components are multiplied with `k`:
- `(x/y/z)*k = (k*x/k*y/k*z)`

Examples:
- `(3/4/5)*2 = (6/8/10)`
- `(1/-2/0)*3 = (3/-6/0)`

The order does not matter:
- `(x/y/z)*k = k*(x/y/z) = (k*x/k*y/k*z)`

You can divide by multiplying with its inverse:
- `(4/6/1)/2 = (4/6/1)*0.5 = (2/3/0.5)`


### Geometrical

Multiplying a Vector with a Scalar value `k` has the following effects:

As for the direction, it
- retains its direction, if `k` is positive
- flips its direction, if `k` is negative
- converts the vector to a zero vector without direction, if `k` is zero

As for the magnitude, it
- scales its magnitude by the absolute value of `k`
  - multiplying a Vector with `2` doubles its magnitude
  - multiplying a Vector with `-2` also doubles its magnitude
  - multiplying a Vector with `0.5` halves its magnitude
  - multiplying a Vector with `0` sets its magnitude to zero

## Scalar Division

As mentioned above, a Division by `k` can be seen as a Multiplication with `(1/k)`.

Besides that
- you can Divide a Vector `v` by a Scalar Value `k` by dividing each component by `k`
- but you can not divide a scalar value `k` by a vector `v`
  - even though you can multiply `(1/k)*v`

## Adding Vectors

We can add two Vectors, if they are of the same Dimension (contain the same amount of numbers)

### Mathematical

Adding Vector `v` and `u` results in a new Vector where each component has been added:
- `u+v = (xu/yu/zu)+(xv/yv/zv) = (xu+xv/yu+yv/zu+zv)`

Examples:
- `(3/1/2)+(10/20/30) = (13/21/32)`
- `(3/0/-2)+(1/7/8) = (4/7/6)`

Addition is Commutative:
- `v+u = u+v`

### Geometrical

If you add Vector `v` and `u`, then geometrically you:
- draw Vector `v` in a coordinate system
- draw Vector `u` at the Head of `v`
  - with the Tail of `u` being at the Head of `v`
  - and the Head being where ever the Vector points to

The resulting Vector `v+u` now is the Vector
- whose Tail is at the Position of the Tail of `v`
- whose Head is at the Position of the Head of `u`

### Combination of Displacements

The Sum of two Vector basically is the combination of Displacements. e.g.:
- `v(5/0)` goes 5 on the positive side of x
- `u(-2/0)` goes 2 on the negative side of x (basically backwards)
- `u+v = (3/0)` goes only 3 steps on the positive side of x

Any Vector is a combination of displacements on each axis:
- `v(3/4/2)` is a Combination of:
  - `(3/0/0)`, a displacement by 3 on the x-axis
  - `(0/4/0)`, a displacement by 4 on the y-axis
  - `(0/0/2)`, a displacement by 2 on the z-axis
- `(3/4/2)` is the sum of above three vectors

## Subtracting Vectors

We can subtract one Vector from another, if they are of the same Dimension (contain the same amount of numbers)

### Mathematical

Adding Vector `u` from `v` results in a new Vector where each component has been subtracted:
- `v-u = (xv/yv/zv)+(xu/yu/zu) = (xv-xu/yv-yu/yv-yu)`

Examples:
- `(7/3/2)-(3/1/2) = (4/2/0)`
- `(3/0/-2)-(-2/2/3) = (5/-2/-5)`

Subtraction is Non-Commutative:
- `v-u != u-v`
- `v-u = -(u-v)`

### Geometrical

If you subtract Vector `u` from `v`, then geometrically you:
- draw Vector `v` in a coordinate system
- draw Vector `u` at the Tail of `v`
  - with the Tail of `u` being at the Tail of `v`
  - and the Head being where ever the Vector points to

The resulting Vector `v-u` now is the Vector
- whose Tail is at the Position of the Head of `u`
- whose Head is at the Position of the Head of `v`

### Difference/Displacement from one Point to Another

When subtracting two Points `v-u`, where
- `v` describes the displacement from the Origin to Point V
- `u` describes the displacement from the Origin to Point U

Then the resulting Vector `v-u` describes
- The displacement from Point U to V
- i.e. the direction + distance from U to V

This is one of the definitions of Vectors:
- the subtraction of two Points

## Vector Magnitude

We have already defined Vectors as being a Combination of Direction and Magnitude. But what is the Magnitude of a Vector like `(3/4)`?

### Mathematical

For a Vector `v` of any Dimensions its 2-norm magnitude `||v||` is:
- the Square Root of the Sum of its Squared Components.

Examples:
- `||(3/4)|| = √(3*3+4*4) = √(9+16) = √(25) = 5`
- `||(3/0/0)|| = √(3*3+0+0) = √(9) = 3`
- `||(5,-3,2)~~ = √(25+9+4) = √(38) ≈ 6.16`

### Geometrical

Geometrically, you can recognize above formula for a Two-Dimensional Vector using Pythagoras' Theorem:

The Vector `(3/4)` is a Sum of Two Displacements:
- `(3/0)` as the `x`-displacement from the Origin along the `x`-axis.
- `(0/4)` as the `y`-displacement from the Head of the previous part along the `y`-axis.
- `(3/4)` is the Vector from the Origin to the Head of the previous part.
- There is a right angle between the `x`-displacement and the `y`-displacement.
- Therefore, `(3/4)` shapes the Hypotenuse of a right triangle.


Pythagoras says that you can define `a*a + b*b = c*c` for:
- `a,b` which are the edges next to the right-angle
- `c` which is the hypotenuse of the triangle

Therefore:
- `3*3 + 4*4 = (||(3/4)||)^2` You can take the Square Root from that:
- `√(3*3+4*4) = ||(3/4)||` Which is the same as the first example above!
- `√(25) = ||(3/4)||`
- `||(3/4)|| = 5`

For any Magnitude `m`, there is an infinite amount of Vectors with the same Magnitude.\
- If you put all those Vectors to the same point with their Tails inwards
- They shape a Circle with Radius `m`

### Square Magnitude

Whenever you want to compare Vectors' magnitudes, e.g. to find out, whether one Vector is smaller than another, you can save a lot of Performance by not taking the Square Root:

- Vector a Magnitude: `5`
- Vector b Magnitude: `4`
- `||a|| > ||b||`

- Vector a Square Magnitude: `25`
- Vector b Square Magnitude: `16`
- `||a||² > ||b||²`

Mathematically, the difference is:
- Square Magnitude: `x*x + y*y + z*z`
- Magnitude: `√(x*x + y*y + z*z)`

In other words, we can skip calculating the `√` SquareRoot! That's a huge performance benefit!

## The Distance Formula

We have enough Knowledge now to start deducting our first own, very useful Vector Formula!

When you want to determine the Distance between to Points, then:
- You can calculate the Displacement between both points by calculating the Difference of the Vectors
  - The Displacement contains both Direction and Magnitude
- And then calculate that Vector's Magnitude
  - The Direction won't matter in that case
    - since the Distance from A to B
    - is the same as from B to A

Distance A <-> B:
- `||(A-B)||`

Example:
- `A: (5/5)`
- `B: (8/1)`

Calculation:
- `||(A-B)||`
- `||(5/5)-(8/1)||`
- `||(-3/4)||
- `√((-3)*(-3)+4*4)`
- `√(9+16)`
- `√(25)`
- `5`

The distance between point A and B is `5`!

## Unit Vector

A Vector consists of Magnitude and Direction. By eliminating the Magnitude of a Vector from the Equation, we end up with the Direction of a Vector.

### Mathematical

A Unit Vector is a Vector with
- a magnitude of `1`

### Normalizing a Vector

A Vector of any magnitude can be converted to a Unit Vector by dividing it by its magnitude:
- `v/||v||`

Example:
- `(3/4)` has a Magnitude of `5`.
- `(3/4) / ||(3/4)||` should be the Unit Vector in the same Direction.
  - Remember that Multiplication and Division does not change the direction as long as `k>0`
- `(3/4) / 5`
- `(0.6/0.8)` is the Result. Let's calculate it's magnitude.
- `||(0.6/0.8)||`
- `√(0.6*0.6+0.8*0.8)`
- `√(0.36+0.64)`
- `√(1)`
- `1` Which is the magnitude that we'd expect from a Unit Vector.

### Geometrical

When drawing a Unit Circle, a Circle with radius `1`, which is used in Trigonometry a lot, then for every Unit Vector:
- if you place the Tail at the Center of the Unit Circle
- the Head will end on the edge of the Unit Circle

## Dot Product

There is two methods for calculating the product of two Vectors. The first method returns a scalar value which denotes the degree to which two vectors share direction and magnitude.

The Dot Product can be found all over video game programming. In all fields including Graphics, Simulation and AI.

### Mathematical

The result of `a⋅b` is the sum of each of its components multiplied:
- `a⋅b = (xa/ya/za)⋅(xb/yb/zb) = xa*xb+ya*yb+za*zb`

Example:
- `(4/6/3)⋅(-1/8/0) = 4*(-1)+6*8+3*0 = -4+48+0 = 44`

### Geometrical

#### Signed Length of Projection

Before understanding the next explanation, it is important to understand that two Vectors `a` and `b` can always be placed to build a Triangle by putting both Vectors together at their tails. You got three points now:
- the shared tail point
- the head point of Vector `a`
- the head point of Vector `b`

Every Triangle is guaranteed to have a surface plane, meaning that it defines a two-dimensional surface on which all three points lie.

From that point of view, you can always align the view on two Vectors so that you can draw both Vectors on that surface on a sheet of paper. On that surface, the following formula applies:

For two Vectors, any vector `a` and any unit Vector `b`, `a⋅b` is:
- the signed length of the projection of `a` onto `b`

The result gives us a general classification for the relative direction between two Vectors:
- a result `||a|| <= a⋅b < 0` means, that the Vectors `a` and `b` go into opposite directions
  - meaning, that the angle between them is more than 90 degrees
- a result `a⋅b == 0` means, that the Vectors `a` and `b` run perpendicular to each other
  - meaning, that the angle between them is exactly 90 degrees
- a result `||a|| > a⋅b > 0` means, that the Vectors `a` and `b` go into similar directions
  - meaning, that the angle between them is less than 90 degrees

Example:
- Unit Vector `b(0.6/0.8)`
- Vector `a(3/4)` goes exactly in the same direction and has Magnitude `5`
  - `a⋅b = 3*0.6+4*0.8 = 1.8+3.2 = 5`
    - `> 0` means, that it goes into the same direction
- Vector `a(-6/-8)` goes exactly in the opposite direction with a magnitude of `10`
  - `a⋅b = (-6)*0.6+(-8)*0.8 = (-3.6) + (-6.4) = -10`
    - `< 0` means, that it goes into the opposite direction
- Vector `a(-4/3)` goes exactly perpendicular with a magnitude of `5`
  - `a⋅b = (-4)*0.6+3*0.8 = -2.4+2.4 = 0`
    - `= 0` means, that it goes perpendicular
- Vector `a(4,3)` goes somewhat in the same direction with a magnitude of `5`
  - `a⋅b = 4*0.6+0.8*3 = 2.4+2.4 = 4.8`

#### Scaling a Vector

If you scale any of the Vectors `a` or `b` with `k`, then the result `a⋅b` will be `k*(a⋅b)`

If `b` is not a Unit Vector, we could make it one by dividing it by its magnitude:
- `b/||b||`

This ensures that the result of `a⋅b` will be as described above:
- the signed length of the projection of `a` onto `b`

However, if `b` is not a Unit Vector, the result will be:
- the signed length of the projection of `a` onto `b` multiplied with `||b||` instead

#### The Parallel and Perpendicular Vector

Continuing on the previous part, by multiplying the result of the Dot Product with the Unit Vector `b`, you get the quantity of the Vector `a` that points in the same direction as `b`.

As an easy example, let's assume that the Unit Vector `b` is actually the Vector that points in the direction of the x-Axis:
- `b(1/0)`

For a Vector `a(-3/4)`, `a⋅b` would then be:
- `a⋅b = 3*1+4*0 = -3`
- which is the x-component of the Vector.

If you multiply that with the Unit Vector `b`:
- `a⋅b*b = -3*(1/0) = (-3/0)`
- you get the Vector component of `a` that is parallel to `b`, to the x-Axis.

If you subtract that component from `a`:
- `a-a⋅b*b = (-3/4) - (-3/0) = (0/4)`
- you get the Vector component of `a` that is perpendicular to `b`, to the x-Axis, which is the y-Component.

Let's calculate the dot product of that result and `b`, just to make sure that it's perpendicular:
- `(a-a⋅b*b)⋅b = (0/4)⋅(1/0) = 0*1+4*0 = 0`
- which proves, that the result is perpendicular to `b`

In other words:
- To get the part of a Vector `a` that's parallel to a Unit Vector `b`: `a⋅b*b`
- To get the part of a Vector `a` that's perpendicular to a Unit Vector `b`: `a-a⋅b*b`

#### The angle between two Vectors

If both `a` and `b` are unit Vectors and `a⋅b` is the signed Projection of `a` onto `b`, then:
- `θ` is the angle between `a` and `b`
- trigonometry says: `cos(θ) = adj/hyp`
  - the adjacent side has length `a⋅b`
  - `a` is the unit hypotenuse of a right triangle with length 1
  - `cos(θ) = (a⋅b)/1 = a⋅b`

Ergo: `a⋅b = cos(θ)` IF both Vectors are Unit Vectors.

We know that if we scale any vector by `k`, then the Dot Product will be scaled by `k` as well. Therefore, if we scale both Vectors by their respective magnitude `||a||` and `||b||` in case they're not Unit Vectors, the result will be:
- `a⋅b = cos(θ) * ||a|| * ||b||`

We can shift above formula around and solve for `θ`:
- `a⋅b = cos(θ) * ||a|| * ||b||`
- `a⋅b / (||a|| * ||b||) = cos(θ)`
- `arccos(a⋅b / (||a|| * ||b||)) = θ`

In other words, we can use this formula to calculate the angle between any two Vectors `a` and `b`:
- `θ = arccos(a⋅b / (||a|| * ||b||))`

If you know, that both Vectors are Unit Vectors, the formula becomes a lot easier (this is, why it is often important to ensure that Directional Vectors are Unit Vectors in the context of Graphics & Rendering):
- `θ = arccos(a⋅b)`

## Cross Product

The Cross Product is the last important Vector Function. It is another way of calculating a Product of two Vectors and returns a new Vector which is perpendicular to both previous Vectors.

### Mathematical

For Two Vectors `a(x1,y1,z1)` and `b(x2,y2,z2)`, the Cross Product `a×b` is a new Vector `c`, where:
- `x = y1z2-z1y2`
- `y = z1x2-x1z2`
- `z = x1y2-y1x2`

There is a handy way of remembering this by putting both Vectors as Column Vectors horizontally next to each other and drawing crosses between the components, but you can honestly just google the formula whenever you need it.

### Geometrical

The resulting Vector `a×b` has these Properties:
- the magnitude `||a||*||b||*sin(θ)`
  - where `θ` the angle between `a` and `b`
- a direction perpendicular to the plane shaped by Vector `a` and `b`
  - There is two perpendicular directions:
    - one going from "over" the plane to "under" the plane
    - one going from "under" the plane to "over" the plane
  - To find out, which one you will receive:
    - use the hand that matches your Coordinate System
    - point the thumb towards `a`
    - point the index finger towards `b`
    - where-ever your middle finger points when making a right angle, is where `a×b` will point

You can test this with the cardinal axes, e.g.:
- `x×y` should result in `z`:
  - `x = y1z2-z1y2 = 0*0-0*1 = 0`
  - `y = z1x2-x1z2 = 0*0-1*0 = 0`
  - `z = x1y2-y1x2 = 1*1-0*0 = 1`
  - `z(0/0/1)`