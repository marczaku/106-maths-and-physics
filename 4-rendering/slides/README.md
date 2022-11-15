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