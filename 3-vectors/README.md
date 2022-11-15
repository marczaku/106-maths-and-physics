# Exercises 3 - Vectors

Implement a 3-dimensional `Vector`-`struct` in your Solution's Maths-Project.
- It should be a `struct` since it's a Value-Type.

## 3.1 Definition

Add 3 `public` `float` values for the `X`, `Y` and `Z` Components to the struct.

```cs
Vector vector; // (0, 0, 0)
vector.X = 5; // (5, 0, 0)
vector.Y = .23f; // (5, 0.23, 0)
vector.Z = -2.5f; // (5, 0.23, -2.5)
```

Add a Constructor to the class which takes an argument for each component and assigns each argument to the corresponding component.

```cs
Vector right = new Vector(1f, 0f, 0f); // (1, 0, 0)
```

## 3.2 Zero Vector

Add a static Property named `Zero` of Type `Vector` with a `get` Accessor. It should return a `Vector` on which all components have the value `0f`.

```cs
Vector acceleration = Vector.Zero; // (0, 0, 0)
// ...
if(velocity == Vector.Zero){
  // ...
}
```

## 3.3 Negating

Add an instance Property named `Inverse` of Type `Vector` with a `get` Accessor. It should return a negated Vector for the Vector on which the `Inverse`-Property is called.

```cs
Vector right = new Vector(1f, 0, 0);
Vector left = right.Inverse; // (-1, 0, 0)
```

## 3.4 Scalar Multiplication

Add an instance Method named `MultiplyWith` with an argument of Type `float`. The Method returns a new `Vector` in which each of the instance's components is multiplied with the `float` Argument passed into the Method.

```cs
Vector right = new Vector(1f, 0, 0);
float movementSpeed = 5f;
Vector movement = right.MultiplyWith(movementSpeed); // (5, 0, 0)
```

## 3.5 Scalar Division

Add an instance Method named `DivideBy` with an argument of Type `float`. The Method returns a new `Vector` in which each of the instance's components is divided by the `float` Argument passed into the Method.

```cs
Vector right = new Vector(1f, 0, 0);
float fps = 50;
Vector movement = right.DivideBy(fps); // (0.02, 0, 0)
```

## 3.6 Addition

Add an instance Method named `Add` with an argument of Type `Vector`. The Method returns a new `Vector` in which the argument Vector is added to the instance Vector.

```cs
Vector position = new Vector(12, 3, -2);
Vector movement = new Vector(2, -1, 0);
position = position.Add(movement); // (14, 2, -2)
```

## 3.7 Subtraction

Add an instance Method named `Subtract` with an argument of Type `Vector`. The Method returns a new `Vector` in which the argument Vector is subtracted from the instance Vector.

```cs
Vector playerPosition = new Vector(12, 3, -2);
Vector enemyPosition = new Vector(14, 1, -2);
Vector directionToEnemy = enemyPosition.Subtract(playerPosition); // (2, -2, 0)
```

## 3.8 Magnitude

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

## 3.9 Distance

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

## 3.10 Unit Vector

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

## 3.11 Dot Product

Add an instance Member named `Dot` with an argument of Type `Vector`. The Method returns a `float` which is the result of the Dot Product of the argument Vector with the instance Vector.

```cs
Vector a = new Vector(1, -2, 4);
Vector b = new Vector(-2, 3, 0.5f);
float dot = a.Dot(b); // -6
```

Add a static Member named `AngleBetweenRad` with two arguments of Type `Vector`. The Method returns a `float` which is the angle between both given Vectors in radians.

```cs
Vector a = new Vector(5, 0, 0);
Vector b = new Vector(3, 3, 0);
float angle = Vector.AngleBetweenRad(a, b); // 0.5·√2 ≈ 0.7071067811865476
```

Add a static Member named `AngleBetweenDeg` with two arguments of Type `Vector`. The Method returns a `float` which is the angle between both given Vectors in degrees.

```cs
Vector a = new Vector(5, 0, 0);
Vector b = new Vector(3, 3, 0);
float angle = Vector.AngleBetweenDeg(a, b); // 45
```

## 3.12 Cross Product

Add an instance Member named `Dot` with an argument of Type `Vector`. The Method returns a `Vector` which is the result of the Cross Product of the instance Vector with the argument Vector.

```cs
Vector right = new Vector(1, 0, 0);
Vector up = new Vector(0, 1, 0);
Vector forward = right.Cross(up); // (0, 0, 1)
```

## 3.13 Bonus: Operators

Implement the usual mathematical operators:

```cs
Vector movement = 2.5f * new Vector(1, 0, 0);
movement *= 2;
movement /= 0.5f;
movement += new Vector(0, 1, 0);
movement -= new Vector(0, 0, 1);
bool isEqual = movement == new Vector(12, -2, 1);
bool isInEqual = movement != new Vector(12, -2, 1);
```