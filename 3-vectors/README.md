# Exercises 3 - Vectors

Implement a 3-dimensional `Vector`-`struct` in your Solution's Maths-Project.
- It should be a `struct` since it's a Value-Type.

## Definition

Add 3 `public` `float` values for the `X`, `Y` and `Z` Components to the struct.

```cs
Vector vector;
vector.X = 5;
vector.Y = .23f;
vector.Z = -2.5f;
```

Add a Constructor to the class which takes an argument for each component and assigns each argument to the corresponding component.

```cs
Vector right = new Vector(1f, 0f, 0f);
```

## Zero Vector

Add a static Property named `Zero` of Type `Vector` with a `get` Accessor. It should return a `Vector` on which all components have the value `0f`.

```cs
Vector acceleration = Vector.Zero;
// ...
if(velocity == Vector.Zero){
  // ...
}
```

## Negating

Add an instance Property named `Inverse` of Type `Vector` with a `get` Accessor. It should return a negated Vector for the Vector on which the `Inverse`-Property is called.

```cs
Vector right = new Vector(1f, 0, 0);
Vector left = right.Inverse; // (-1, 0, 0)
```

## Scalar Multiplication

Add an instance Method named `MultiplyWith` with an argument of Type `float`. The Method returns a new `Vector` in which each of the instance's components is multiplied with the `float` Argument passed into the Method.

```cs
Vector right = new Vector(1f, 0, 0);
float movementSpeed = 5f;
Vector movement = right * movementSpeed; // (5, 0, 0)
```

## Scalar Division

Add an instance Method named `DivideBy` with an argument of Type `float`. The Method returns a new `Vector` in which each of the instance's components is divided by the `float` Argument passed into the Method.

```cs
Vector right = new Vector(1f, 0, 0);
float fps = 50;
Vector movement = right / fps; // (0.02, 0, 0)
```

## Addition

Add an instance Method named `Add` with an argument of Type `Vector`. The Method returns a new `Vector` in which the argument Vector is added to the instance Vector.

```cs
Vector position = new Vector(12, 3, -2);
Vector movement = new Vector(2, -1, 0);
position = position.Add(movement); // (14, 2, -2)
```

## Subtraction

Add an instance Method named `Subtract` with an argument of Type `Vector`. The Method returns a new `Vector` in which the argument Vector is subtracted from the instance Vector.

```cs
Vector playerPosition = new Vector(12, 3, -2);
Vector enemyPosition = new Vector(14, 1, -2);
Vector directionToEnemy = enemyPosition.Subtract(playerPosition); // (2, -2, 0)
```

## Magnitude

Add an instance Property named `Magnitude` with a `get` Accessor. The Method returns a `float` which is the value of the Vector's magnitude.

```cs
Vector playerPosition = new Vector(3, 4, 0);
float magnitude = playerPosition.Magnitude; // 5
```

Add an instance Property named `SquareMagnitude` with a `get` Accessor. The Method returns a `float` which is the value of the Vector's squared magnitude.

```cs
Vector playerPosition = new Vector(3, 4, 0);
float magnitude = playerPosition.Magnitude; // 25
```

## Distance

Add an instance Method named `DistanceTo` with an argument of Type `Vector`. The Method returns a `float` which is the 2-norm distance of the given Vectors.

```cs
Vector playerPosition = new Vector(3, 4, -2);
Vector enemyPosition = new Vector(9, 4, 6);
float distance = playerPosition.DistanceTo(enemyPosition); // 10
```

Add an instance Method named `SquaredDistanceTo` with an argument of Type `Vector`. The Method returns a `float` which is the square of the 2-norm distance of the given Vectors.

```cs
Vector playerPosition = new Vector(3, 4, -2);
Vector enemyPosition = new Vector(9, 4, 6);
float distance = playerPosition.SquaredDistanceTo(enemyPosition); // 100
```

## Unit Vector

Add an instance Property named `Normalized`. The Method returns a new `Vector` with a magnitude of `1` but the same direction as the instance Vector.

```cs
Vector enemyDisplacement = new Vector(4, 0, 3);
Vector enemyDirection = enemyDisplacement.Normalized; // (0.8, 0. 0.6)
```

Add an instance Property named `IsUnitVector`. The Method returns a `bool` which returns `true`, if the given instance Vector is a Unit Vector.

```cs
bool isUnitVector = new Vector(3, -1, 0).IsUnitVector; // false
isUnitVector = new Vector(-1, 0, 0).IsUnitVector; // true
```

## Dot Product

Add an instance Member named `Dot` with an argument of Type `Vector`. The Method returns a `float` which is the result of the Dot Product of the argument Vector with the instance Vector.

```cs
Vector a = new Vector(1, -2, 4);
Vector b = new Vector(-2, 3, 0.5f);
float dot = a.Dot(b); // -6
```

Add a static Member named `AngleBetween` with two arguments of Type `Vector`. The Method returns a `float` which is the angle between both given Vectors in radians.

```cs
Vector a = new Vector(5, 0, 0);
Vector b = new Vector(3, 3, 0);
float angle = Vector.AngleBetween(a, b); // 0.5·√2 ≈ 0.7071067811865476
```

Add a static Member named `AngleBetweenDeg` with two arguments of Type `Vector`. The Method returns a `float` which is the angle between both given Vectors in degree.

```cs
Vector a = new Vector(5, 0, 0);
Vector b = new Vector(3, 3, 0);
float angle = Vector.AngleBetween(a, b); // 45
```