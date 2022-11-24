# Slides 5 - Matrices

## Coordinate Spaces

Useful:
- a map of Berlin puts 0/0 in the middle of Uppsala
- a map of Stockholm put 0/0 in the middle of Stockholm
- what, if you want to draw a map including both?

### World Space
- Real World: east, west, north, south
- a.k.a global space, universal space
- but only in a given context
- e.g. a Video Game in New York wouldn't put their game objects as far away from 0/0 as New York is from 0˚00' North 0˚00' West

### Object Space
- Real World: forward, back, left right
- you carry your personal coordinates with you:
  - over you
  - behind you
- a.k.a. model space, body space

### Camera Space
- World as seen through a camera
- "up" may be "left", if camera is tilted

### Screen Space
- Flat, two-dimensional
- requires projection

### Upright Space
- a.k.a. Global Gizmos (Unity)
- origin = object space
- orientation = world space

### Coordinate Space Transformations
- One meter in front of me
- One meter North-East
- At 56˚00' North 27˚00' West

### Dual Perspective
- Moving the Origin around
- Moving all Points around the Origin

### Specifying Coordinate Spaces
- Unit Axes
  - World Right `p`: `x: 1, y: 0, z: 0`
  - World Up `q`: `x: 0, y: 1, z: 0`
  - World Forward `r`: `x: 0, y: 0, z: 1`
- Origin
  - World: `x: 0, y: 0, z: 0`

`v = xp + yq + zr`

### Choosing wisely
- should be perpendicular

`u = x*p + y*q + z*r`

```
u.x = x*p.x + y*q.x + z * r.x
u.y = x*p.y + y*q.y + z * r.y
u.z = x*p.z + y*q.z + z * r.z
```

> The numeric coordinates of a vector with respect to a given basis are the coefficients in the expansion of that vector as a linear combination of the basis vectors.

> When the basis vectors are orthogonal, the coordinates are uncoupled. Any given coordinate of a vector v can be determined solely from v.

### Nested Space
- Where are a sheep's ears relative to its head?
- Where is the head relative to the body?
- Where is the body relative to the world's origin?

## Matrices

### Mathematical
A rectangular grid of numbers arranged in rows and columns.

#### Dimensions

- 4x4, 4x3, 3x3, 3x2

#### Square Matrix

#### Diagonal Matrix

#### Identity Matrix

#### Vectors as Matrices

#### Matrix Transposition

```
1 2 3
4 5 6
7 8 9
A B C
```

Becomes

```
1 4 7 A
2 5 8 B
3 6 9 C
```

#### Scalar Multiplication

#### Matrix Multiplication

Non-Commutative:
- `A*B != B*A`

#### Vector Multiplication

Each element in the resulting Vector is the dot product of the original vector with a single row or column of the matrix

Each element in the matrix determines the "weight" of a element in the vector in the output vector

#### Row versus Column Vectors
- DirectX uses row vectors
- OpenGL uses column vectors
  - other sciences do, too!

### Geometrical

- Matrix = Basis Vectors + Translation
- Rotation
- Scale
- Orthographic Projection
- Reflection
- Shearing

Rows of a Matrix: Basis Vectors of a Coordinate Space

## Linear Transformations
- Do not contain translations
- Any transformation can be accomplished with matrix multiplication

## Affine Transformations
- Linear Transformation followed by translation

### Invertible Transformation
- Can be undone

### Angle-Preserving Transformation
- angle between vectors is not altered in either magnitude or direction

### Orthogonal Transformation
- Base Vectors are orthonormal basis

### Rigidbody Transformation
- changes location and orientation, but not shape

## Determinant

## Inverse

## Translation: 4D