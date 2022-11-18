# Exercises 4 - Rendering

[Here's The Slides!](slides/README.md)

## Scaling Up
Use `MultiplyWith(1.01f)` to scale up your triangle while pressing H
## Scaling Down
Use `DivideBy(1.01f)` to scale down your triangle while pressing G
## Moving Around
Use `Add(new Vector(...))` to move your triangle around while pressing WASD
## Question
What happens, if you move the triangle to an edge and then scale it up/down? How can you explain it?
## Change the Fragment Shader
Change the Triangle's color to be blue.
## Bonus: Now there's two of them!
Put a second triangle on the screen
## Bonus: Rotation
Rotate the Triangle continuously around itself.
## Clean Up Code: Window
Introduce a `Window`-class to handle the Window Logic:
```cs
public interface IWindow
{
    /// <summary>
    /// Returns true, if the user or anyone else has requested to close the Window.
    /// </summary>
    bool ShouldClose{get;}
    
    /// <summary>
    /// Checks, whether the current state of the key provided is Press or Repeat.
    /// </summary>
    /// <param name="key">The key to check for.</param>
    /// <returns>`true`, if the key is currently being pressed.</returns>
    bool GetKey(Keys key);

    /// <summary>
    /// Polls Window Events and clears the active buffer
    /// </summary>
    void BeginRender();

    /// <summary>
    /// Swaps the buffers, presenting the current frame to the display.
    /// </summary>
    void EndRender();
```

Your class should furthermore have the following fields and methods:
```cs
/// <summary>
/// Used to store the Window Handle. It is needed for all kind of functions that handle the window's state.
/// </summary>
private readonly GLFW.Window _window;

/// <summary>
/// Initializes and opens a new OpenGL Window.
/// - initializes GLFW
/// - configures and creates a window
/// - sets the window to current context
/// - imports the dynamically linked GL functions
/// - connects the key callback for closing the window on Esc
/// </summary>
public Window(){/*...*/}

/// <summary>
/// Invoked by GLFW whenever a key is pressed.
/// Closes the Window, if Esc was pressed.
/// </summary>
/// <param name="window">Pointer of the window that registered the event</param>
/// <param name="key">The key being pressed</param>
/// <param name="scanCode">system-specific scancode of the key</param>
/// <param name="state">The new state of the key (pressed, repeat, released)</param>
/// <param name="mods">Modifier keys like Alt, Shift, ....</param>
private OnKeyCallback(System.IntPtr window, Keys key, int scanCode, InputState state, ModifierKeys mods){/*...*/}
```
## Clean Up Code: Material
Introduce a `Material`-class to handle the Shader Program logic:
```cs
public interface IMaterial {
    /// <summary>
    /// Sets up the GL Context to use this Material's Shader Program.
    /// </summary>
    void Use();
}
```

Your class should furthermore have the following fields and methods:

```cs
/// <summary>
/// Used to store the Shader Program Handle. It is needed in order to use it for rendering.
/// </summary>
private uint shaderProgram;

/// <summary>
/// Initializes this Material.
/// Creates and compiles a vertex shader.
/// Creates and compiles a fragment shader.
/// Attaches both to a Shader Program and links it.
/// </summary>
public Material(){/*...*/}
```

## Clean Up Code: Mesh

Introduce a `MeshRenderer`-class to handle the vertices and rendering a Mesh to the screen.

```cs
public interface IMesh {
    /// <summary>
    /// Renders the mesh to the screen.
    /// - binds the Vertex Array Object.
    /// - draws the vertex arrays.
    /// </summary>
    void Render();
}
```

Your class should furthermore have the following fields and methods:

```cs
/// <summary>
/// A Buffer Array for storing the vertices on the RAM;
/// </summary>
private Vector[] vertices
/// <summary>
/// The Vertex Array Object is an object that represents the vertex fetch stage of the OpenGL pipeline and is used to supply input to the vertex shader. It will store vertex buffer objects as well as the vertex attribute configuration.
/// </summary>
private uint _vertexArrayObject;
/// <summary>
/// A Vertex Buffer Object is an OpenGL feature that provides methods for uploading vertex data (position, normal vector, color, etc.) to the video device for non-immediate-mode rendering.
/// </summary>
private uint _vertexBufferObject;
/// <summary>
/// Creates and initializes Vertex Buffer and Array Object.
/// Adds vertex data to the Vertex Buffer.
/// Configures and enables Vertex Attributes.
/// </summary>
public Mesh(){/*...*/}
```

