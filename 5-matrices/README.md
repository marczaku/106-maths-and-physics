# Exercises 5 - Matrices

[Here's The Slides!](slides/README.md)

## Code Clean-Up: Transform

Introduce a `Transform`-class to handle the Matrix Calculations.

```cs
/// <summary>
/// Sets the Translation from the Origin of this Transform.
/// </summary>
public Vector Position { get; set; }
/// <summary>
/// Sets the Euler-Angles of the Rotation of this Transform in Radians.
/// </summary>
public Vector Rotation { get; set; }
/// <summary>
/// Sets the Scale along the Base Vectors.
/// </summary>
public Vector Scale { get; set; }
/// <summary>
/// Returns a TRS-Transformation-Matrix for this Transform.
/// </summary>
public Matrix Matrix {get{/*...*/}}

/// <summary>
/// Initializes this Transform with Default Values.
/// </summary>
public Transform() : this(/*...*/){}
/// <summary>
/// Initializes this Transform with Custom Values.
/// </summary>
public Transform(Vector position, Vector rotation, Vector scale){/*...*/}

/// <summary>
/// Changes the Transform's Rotation by the given Euler-Angles.
/// </summary>
/// <param name="rotation">Euler-Angles in Radians</param>
public void Rotate(Vector rotation){/*...*/}

/// <summary>
/// Changes the Transform's Position by the given Displacement
/// </summary>
/// <param name="displacement">Displacement on each Axis</param>
public void Move(Vector displacement){/*...*/}
```

## Clean Up: Shader Source

Move the Shader Source Code to separate files.

### Vertex Shader
- Add a new Folder `shaders` to your Engine Project
- Add a new File `world-space.vert` for our Vertex Shader Code
  - Install the GLSL Support Plugin if Rider asks you
- In the Material class, cut out the string after `const string vertexShaderCode = @"`
- Paste it into the File `world-space.vert`
- In the Material class, replace the `const string vertexShaderCode` with `string vertexShaderCode = File.ReadAllText("shaders/world-space.vert");`
  - Above code opens and fully reads the contents of a file into a string
- In the `shaders` Folder, add another File `orange.frag` for our Fragment Shader Code
- In the Material class, cut out the string after `const string fragmentShaderCode = @"`
- Paste it into the File `orange.frag`
- In the Material class, replace the `const string fragmentShaderCode` with `string fragmentShaderCode = File.ReadAllText("shaders/orange.frag");`

## Clean Up: Let the GPU Move Vertices

Add a new Shader named `object-space.vert` that can handle Object Space Transformations:

```c
#version 330 core
layout (location = 0) in vec3 pos;
layout (location = 1) in vec4 color;

out vec4 vertexColor;

uniform mat4 transform;

void main()
{
    gl_Position = transform * vec4(pos.x, pos.y, pos.z, 1.0);
    vertexColor = color;
}
```

Add a new `public` Method named `SetTransform` on your `Material` class that allows assigning a `Matrix` to the `Transform` Property on the Shader:

```cs
int transformLocation = glGetUniformLocation(this.program, "transform");
glUniformMatrix4fv(transformLocation, 1, true, &matrix.m11);
```

- Make sure to change the Path to the new Vertex Shader in your `Material` constructor.
- Make sure to not update the `vertices` every time before rendering anymore (in the `Mesh`)
- Instead, assign the current `Transform.Matrix` to the `Material`
- This will require you to pass a `Material` to the `Mesh` constructor and cache it as a field
