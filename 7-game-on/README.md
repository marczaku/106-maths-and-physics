# Prerequisites:

## Vertex Array Object

Ensure that the `MeshRenderer` activates its `VertexArrayObject` before Rendering. The Vertex Array Object holds all Vertex Information (Configuration and Buffers) and we need to bind it to ensure that OpenGL knows, what Mesh we'd like to render right now.

The following line of code should be placed in `MeshRenderer.Render` before `glDrawElements(...)`:

```cs
glBindVertexArray(_vertexArrayObject);
glDrawEle...
```

## Matrix.FromBaseVectors

You can create a Matrix by providing all three base Vectors (the directions in which `x`,`y` and `z` axes point).

Add the Following Method to your `Matrix` class:

```cs
public static Matrix FromBaseVectors(Vector xAxis, Vector yAxis, Vector zAxis)
{
    Matrix result = Identity;
    result.m11 = xAxis.x;
    result.m21 = xAxis.y;
    result.m31 = xAxis.z;

    result.m12 = yAxis.x;
    result.m22 = yAxis.y;
    result.m32 = yAxis.z;

    result.m13 = zAxis.x;
    result.m23 = zAxis.y;
    result.m33 = zAxis.z;

    return result;
}
```

## Transform.Rotation

We need more control for the `Transform.Rotation`. More specifically, we want to be able to assign a `Matrix` instead of a `Vector`.

This can be done quite easily by replacing the Field:

```cs
// instead of:
// public Vector Rotation;
// do:
public Matrix Rotation = Matrix.Identity;
```

Now, the code that rotates your cube won't compile anymore. But that can be fixed quite easily:

```cs
// cube.Rotation = cube.Rotation.Add(new Vector(deltaTime, deltaTime, 0f));
cube.Rotation = Matrix.Rotation(new Vector(deltaTime, deltaTime, 0f)) * cube.Rotation;
```

Also, the code that rotates the Player camera won't compile anymore. You need to do almost the same as above, but using `deltaCursorX` and `deltaCursorY` instead. In order for the rotation to be bug free, you also need to do the following:

```cs
transform.Rotation = /*create rotation from deltaCursorX*/ * transform.Rotation * /*create rotation from deltaCursorY*/;
```

The reason for that is that you need to keep the rotations in the correct order (x rotations before y rotations etc.) and since the `transform.Rotation` contains both rotations, doing them in this order will yield the correct result. If you don't do it this way, the rotation will behave really weird if looking up and then rotating left-right. Try it out with the following code:

```cs
transform.Rotation = /*create rotation from deltaCursorX*/ * /*create rotation from deltaCursorY*/ * transform.Rotation;
```


# Passing Criteria:

## Add a New Feature: (F)ocus Cube

While the Player is holding the `F`-Key:
- `A` and `D` lets the player move left and right.
  - relative to his own axes
- `W` and `S` lets the player move up and down.
  - relative to his own axes
- The Camera always looks directly at the Cube without Rolling.
  - Use the Cross Product to 

Otherwise:
- `A` and `D` lets the player move left and right.
  - relative to his own axes
- `W` and `S` lets the player forward and backward.
  - relative to his own axes
- Moving the Mouse on the X-Axis lets the player look left and right.
  -
- Moving the Mouse on the Y-Axis lets the player look up and down.

## Add a Hint of Physics:
- Add Gravity, which makes the Player fall towards the Plane
  - The Player needs a Velocity that you need to update
  - Each Frame, the Velocity changes the Player's Position
    - Don't forget to use DeltaTime
  - Each Frame, Gravity changes the Player's Velocity by adding Down Force
    - Don't forget to use DeltaTime
- Stop the Players Fall when he is on height of the Plane
  - Tip: Just check the Position's Coordinate and Clamp it
  - Add a little Offset, so it doesn't look like the Player's a Mouse
  - Reset the Player's Velocity
- Allow the Player to jump when he presses `Space`
  - Change the Velocity so it makes the Player move Up
- Disable Gravity while the player is holding the `F`-Key
  - (The player can float while he's aiming at the Cube)
  - (A bit like a Gravity Ray)

# Excellent Criteria:

## Add a new Object:
- Add a `PyramidMesh` that looks like a Pyramid.
  - Use a proper UV-Layout with the `Wall`-Texture
  - The edges will most likely not be seamless.
- Add a `MeshRenderer` that renders said `PyramidMesh`.
- Make that Pyramid orbit around the Cube in the Center.
- Make that Pyramid also turn around its own axis