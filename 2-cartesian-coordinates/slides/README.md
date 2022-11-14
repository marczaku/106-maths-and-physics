# Slides 2 - Cartesian Coordinates

## Dimensions

Cartesian Coordinate Systems can have `n` dimensions. They can for example be one-dimensional, two-dimensional or three-dimensional, but also forty-dimensional.

## Axes

Cartesian Coordinate Systems contain one axis for each dimension. Each axis has a direction, denoted by an arrow head.

They are usually named `x`, `y`, `z`, `w` in that order for the first, second and third dimension.

The axes are usually aligned in perpendicular, e.g:
- `x` pointing to the right
- `y` pointing upwards
- `z` pointing forwards

## Origin

The origin of a cartesian coordinate system is the point in which all axes come together.

## Points

Cartesian Coordinate Systems allow to plot points within the system. A point (4/3) describes the distance along each axis in a coordinate system. In this case:
- `4` units in the positive direction on the `x`-axis
- `3` units in the positive direction on the `y`-axis

They can be plotted in negative directions as well. (-2/-3) would be:
- `2` units in the negative direction on the `x`-axis
- `3` units in the negative direction on the `y`-axis

And they can be point in fractional positions as well. (1.5/3.001) would be:

- exactly in the middle between `1` and `2` units on the `x`-axis
- `1/1000` units from `3` towards `4` on the `y`-axis

## Left-Handed and Right-Handed

3-Dimensional Coordinate Systems can be either Left-Handed or Right-Handed depending on what directions the axes show.

You can test the "Handedness" by pointing your
- Thumb towards positive x
- Index Finger towards positive y
- Middle Finger towards positive z

If it doesn't work, try the other hand.

If it works and you have used your left-hand, you have a Left-Handed Coordinate System and vice versa.

### Left-Handed Example

Unity uses a Left-handed System:

- x: right
- y: up
- z: forward (away from you)

### Right-Handed Example

- x: right
- y: up
- z: backwards (towards you)

### Transforming from one to another

A Left-handed coordinate system can be transformed to a Right-handed one by either: Flipping the positivity on one axis:

- x: right
- y: up
- z: forward (away from you)

Would then for example become:

- x: left
- y: up
- z: forward (away from you)

Or by swapping two axes, so:

- x: right
- y: up
- z: forward (away from you)

Would then for example become:

- y: right
- x: up
- z: forward (away from you)