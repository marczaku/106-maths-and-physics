# Slides 4 - Rendering

## OpenGL

- OpenGL is not an `API` (`Application Programming Interface`)
- It is a specification
  - exactly WHAT the result/output of each function should be
  - developers decide HOW to implement this specification

Developers are usually GPU manufacturers
- Each GPU that you buy supports specific versions of OpenGL
- If OpenGL shows weird behavior, it's usually the GPU manufacturer's fault
- Updating your GPU drivers will often fix the issues

### Core-Profile vs Immediate Mode

Immediate Mode (Fixed Function Pipeline) is an easy-to-use mode of the past
- deprecated since 3.2
- extremely inefficient
- doesn't allow much freedom and flexibility in rendering pipeline
- easy-to-use
- but hard to grasp how OpenGL actually operates

Core-Profile
- forces to use modern practices
- requires to truly understand OpenGL and graphics programming
- allows more flexibility, more efficiency
- throws errors and stops drawing when using deprecated functions

### Versions

- Current Version: 4.6
- Version used here: 3.3
- Changes only add convenience functions
- No major changes to the underlying architecture
- Only the most modern graphics cards will support the latest version!

### Extensions

Won't be relevant for our explorations. But each GPU-Provider can provide their own custom extensions to OpenGL.

### State Machine

OpenGL is a large State Machine.
- collection of variables that define how OpenGL should operate
- referred to as the OpenGL context

We usually use it like this:
- set a variable that tells OpenGL what color to use
- set a variable that tells OpenGL to draw lines
- set a variable that tells OpenGL what positions to draw at
- tell OpenGL to draw

Now, we could:
- set a variable that tells OpenGL what other to draw at
- tell OpenGL to draw

There is
- state-changing functions
  - changing the current context
- state-using functions
  - performing operations based on the current context

### Objects

Objects are managed by OpenGL. We can reference them in C# using ids:

```cs
// generate an object
uint vertexArray = glGenVertexArray();
// bind that object as target of the current context
glBindVertexArray(vertexArray);

// ... operations on that object

// unbind that object
glBindVertexArray(0);
```

### Additional Resources
[Official Website of OpenGL](https://www.opengl.org/)
[Open GL Registry](https://www.opengl.org/registry/)

## Creating a Window

We need to create an OpenGL Context and an Application Window to draw in. Those operations are very Operating System specific, unfortunately.

Luckily, there are cross-platform libraries that already provide that functionality:
- GLUT
- SDL
- SFML
- GLFW

We'll use GLFW.

### GLFW

GLFW is a Library
- written in C
- targeted at OpenGL
- providing bare necessities for rendering
  - create OpenGL Context
  - define window parameters
  - handle user input
  - which is all we need

### Using GLFW

I will hand you a Zip-Archive with multiple files:
- `libglfw.a` & `libglfw.dylib` for UNIX Systems
- `glfw.dll` for Windows Systems
- `OpenGL.cs` as a Wrapper to load those Libraries in .NET

You need to extract those files into your Repository into your `Engine`-Console Project Folder.

And then select the first three files
- Right-click
- Select Properties
- Change `Copy to Output Directory`
  - From `Do not Copy`
  - To `Copy if Newer`

Next, you need to add the dependency `glfw-net` to your project:
```
dotnet add package glfw-net --version 3.3.1
```

## Hello Window

### Create a Window

Alright, first, we need to initialize GLFW:

```cs
using System;
using GLFW;

Console.WriteLine("Starting Engine...");
Glfw.Init();
```

Next, we need to prepare the creation of a Window by informing GLFW of all the OpenGL Settings that we want to work with:

```cs
Glfw.WindowHint(Hint.ClientApi, ClientApi.OpenGL);
Glfw.WindowHint(Hint.ContextVersionMajor, 3);
Glfw.WindowHint(Hint.ContextVersionMinor, 3);
Glfw.WindowHint(Hint.OpenglProfile, Profile.Core);
Glfw.WindowHint(Hint.OpenglForwardCompatible, Constants.True); // Needed on MacOS X
Glfw.WindowHint(Hint.Doublebuffer, Constants.True);
```

Now we're ready to actually create a new window. If it fails, it will return `Window.None`:

```cs
Window window = Glfw.CreateWindow(800, 600, "ForsEngine", Monitor.None, Window.None);
if (window == Window.None)
{
    Console.WriteLine("There has been an unknown error creating the window. Exiting.");
    Glfw.Terminate();
    Environment.Exit(1);
}
```

Now, that we have a Window, we need to make sure to tell OpenGL to use that Window as a Target for our future operations:

```cs
Glfw.MakeContextCurrent(window);
```

And then we're ready to import all functions supported by the exact OpenGL Version currently used by the Window:
```cs
Import(Glfw.GetProcAddress);
```

### Core Loop

Now, we're ready to add our Game Engine's Main Render/Update Loop. This will be the heart of our Game Engine in the future:

```cs
while (!Glfw.WindowShouldClose(window))
{
    // Check and call events
    Glfw.PollEvents();

    // Rendering commands will follow here
    // ...

    // Swap the buffers
    Glfw.SwapBuffers(window);
}
```

### Clean-Up

After the `while`-Loop, we should make sure to clean up OpenGL again:

```cs
Glfw.Terminate();
```

### Handling Input Events

We can add the following code after creating a window, but before the Core Loop to check for input and close the window when `Esc` is pressed:

```cs
Glfw.SetKeyCallback(window, KeyCallback);
    
void KeyCallback(
    IntPtr window,
    Keys key,
    int scanCode,
    InputState state,
    ModifierKeys mods){
    if (key == Keys.Escape && state == InputState.Press)
    {
        Glfw.SetWindowShouldClose(Glfw.CurrentContext, true);
    }
}
```

By using the Key-Callback function, you can react to button press events even if they happen in-between two frames.

There is other callback functions, too:

<details>

`SetWindowMaximizeCallback`
`SetWindowContentScaleCallback`
`SetErrorCallback`
`SetWindowPositionCallback`
`SetWindowSizeCallback`
`SetWindowFocusCallback`
`SetCloseCallback`
`SetDropCallback`
`SetCursorPositionCallback`
`SetCursorEnterCallback`
`SetMouseButtonCallback`
`SetScrollCallback`
`SetCharCallback`
`SetCharModsCallback`
`SetFramebufferSizeCallback`
`SetWindowRefreshCallback`
`SetKeyCallback`
`SetJoystickCallback`
`SetMonitorCallback`
`SetWindowIconifyCallback`

</details>

### Rendering

Let's add our first Rendering Function in the Core Loop under Rendering. This will clear the screen with some violet color:

```cs
glClearColor(.2f, .05f, .2f, 1f);
glClear(GL_COLOR_BUFFER_BIT);
```

### Handling Input State

If you put the following code between the two previous lines of code, you should be able to see the screen brighten up while you're holding down the Space-Key:

```cs
if(Glfw.GetKey(window, Keys.Space) != InputState.Release){
  glClearColor(.4f, .1f, .4f, 1f);
}
```

## Hello Triangle

### Vertex Data

First, we need to create the vertices of the triangle:

```cs
float[] vertices =
{
    -.5f, -.5f, 0f,
    .5f, -.5f, 0f,
    0f, .5f, 0f
};
```

#### Vertex Array

Then, we need to send them to the GPU. For that, we need a Vertex Array (which can hold the Vertex Buffer State):

```cs
uint vertexArray = glGenVertexArray();
glBindVertexArray(vertexArray);
```

#### Vertex Buffer

And also a Vertex Buffer:
```cs
uint vertexBuffer = glGenBuffer();
glBindBuffer(GL_ARRAY_BUFFER, vertexBuffer);
```

Now, we can copy the vertex information to the GPU:

```cs
unsafe
{
    fixed (float* vertex = &vertices[0])
    {
        glBufferData(GL_ARRAY_BUFFER, sizeof(float) * vertices.Length, vertex, GL_STATIC_DRAW);
    }
}
```

And tell the GPU, where it an find what attributes:
```cs
glVertexAttribPointer(0, 3, GL_FLOAT, false, 3 * sizeof(float), IntPtr.Zero);
```

We should always unbind our buffers, so we don't buffer anything into them by accident:
```cs
glBindBuffer(GL_ARRAY_BUFFER, 0);
glBindVertexArray(0);
```

### Shader Program

Before we can draw this triangle, we need to create a Shader Program, though, which is the pipeline of shaders that tell the shader, where and how to print our vertices to the screen:

```cs
shaderProgram = glCreateProgram();
glAttachShader(shaderProgram, vertexShader);
glAttachShader(shaderProgram, fragmentShader);
glLinkProgram(shaderProgram);
{
  int success;
  glGetProgramiv(shaderProgram, GL_LINK_STATUS, &success);
  if (success == GL_FALSE)
  {
      string error = glGetProgramInfoLog(shaderProgram);
      Console.WriteLine("Error linking program: " + error);
  }
}
```

The mentioned shaders need to be compiled from GLSL source code.

#### Vertex Shader

Vertex Shader:

```cs
const string vertexShaderSource = @"
#version 330 core
layout (location = 0) in vec3 position;

void main() {
    gl_Position = vec4(position.x, position.y, position.z, 1.0);
}";

uint vertexShader = glCreateShader(GL_VERTEX_SHADER);
glShaderSource(vertexShader, vertexShaderSource);
glCompileShader(vertexShader);

unsafe {
    int success;
    glGetShaderiv(vertexShader, GL_COMPILE_STATUS, &success);
    if (success == GL_FALSE)
    {
        string error = glGetShaderInfoLog(vertexShader);
        Console.WriteLine("Error compiling shaders: " + error);
    }
}
```

#### Fragment Shader

Fragment Shader:

```cs
const string fragmentShaderSource = @"
#version 330 core
out vec4 color;
void main() {
    color = vec4(1.0f, 0.5f, 0.2f, 1.0f);
}";

uint fragmentShader = glCreateShader(GL_FRAGMENT_SHADER);
glShaderSource(fragmentShader, fragmentShaderSource);
glCompileShader(fragmentShader);

unsafe {
    int success;
    glGetShaderiv(fragmentShader, GL_COMPILE_STATUS, &success);
    if (success == GL_FALSE)
    {
        string error = glGetShaderInfoLog(fragmentShader);
        Console.WriteLine("Error compiling shaders: " + error);
    }
}
```

After linking the Program, we can delete the compiled shaders:

```cs
glDeleteShader(vertexShader);
glDeleteShader(fragmentShader);
```

Now, we can go and draw the triangles in our Render Loop between clearing the screen and swapping the buffers:

```cs
glBindVertexArray(vertexArray);
glUseProgram(shaderProgram);
glDrawArrays(GL_TRIANGLES, 0, 3);
glBindVertexArray(0);
```

## Textures

### Loading a Texture

Install Package
```
dotnet add package SixLabors.ImageSharp --version 2.1.3
```

I'll spare you the details of loading a Texture:

```cs
namespace ForsEngine;

using System;
using System.Buffers;
using static OpenGL.Gl;
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.PixelFormats;
using SixLabors.ImageSharp.Processing;

namespace ForsEngine;

public class Texture
{
    /// <summary>
    /// Stores a reference to the GL Texture Object
    /// </summary>
    private uint textureObject;
    
    /// <summary>
    /// Prepares a Texture for rendering with OpenGL:
    /// - loads the texture to Memory
    /// - creates a GL Texture object
    /// - buffers the texture to the GPU
    /// - generates mip-map levels
    /// - clears up the texture from the RAM
    /// </summary>
    /// <param name="texturePath">The path from which to load the texture.</param>
    public unsafe Texture(string texturePath)
    {
        Configuration customConfig = Configuration.Default.Clone();
        customConfig.PreferContiguousImageBuffers = true;
        
        using Image<Rgb24> image = Image.Load<Rgb24>(customConfig, texturePath);
        image.Mutate(context => context.Flip(FlipMode.Vertical));
        textureObject = glGenTexture();
        glBindTexture(GL_TEXTURE_2D, textureObject);
        
        if (!image.DangerousTryGetSinglePixelMemory(out Memory<Rgb24> memory))
        {
            throw new Exception(
                "This can only happen with multi-GB images or when PreferContiguousImageBuffers is not set to true.");
        }

        using MemoryHandle pinHandle = memory.Pin();
        void* ptr = pinHandle.Pointer;
        glTexImage2D(GL_TEXTURE_2D, 0, GL_RGB, image.Width, image.Height, 0, GL_RGB, GL_UNSIGNED_BYTE, ptr);
        glGenerateMipmap(GL_TEXTURE_2D);
    }

    /// <summary>
    /// Binds the texture to the active GL Texture ren.
    /// Don't forget to use `glActiveTexture(GL_TEXTURE0)` before.
    /// </summary>
    public void Use()
    {
        glBindTexture(GL_TEXTURE_2D, textureObject);
    }
}
```

### Fragment Shader

The following Fragment Shader, `texture.frag`, can sample a texture's pixel if a texture coordinate (x:0-1,y:0-1) has been provided:

```c
#version 330 core

in vec2 TexCoord;

out vec4 color;

uniform sampler2D _texture;

void main() {
    color = texture(_texture, TexCoord);
}
```

### Vertex Shader

As you might have guessed, the `in` parameter needs to be provided by the Vertex Shader, while the `uniform` parameter will be set by our C# Code.

The following shader will just copy the current Vertex's position as a Texture-Coordinate. This admittedly won't be between 0 and 1, but -1 and 1 instead, but this won't be an issue, since the Texture Sampler will just Loop the Texture.

This will give a cool Window-Triangle effect:

```c
#version 330 core
layout (location = 0) in vec3 pos;

out vec2 TexCoord;

uniform mat4 transform;

void main()
{
    gl_Position = transform * vec4(pos, 1.0f);
    TexCoord = vec2(gl_Position.x, gl_Position.y);
}
```