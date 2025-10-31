# Learn-Open-GL

# Source 
[LearnOpenGL](https://learnopengl.com/Introduction)

# Part 1: Getting Started
## 2: OpenGL

> Since most implementations are built by graphics card manufacturers. Whenever there is a bug in the implementation this is usually solved by updating your video card drivers; those drivers include the newest versions of OpenGL that your card supports. This is one of the reasons why it’s always advised to occasionally update your graphic drivers.

## 2.1: Core-profile vs Immediate mode

> When using functionality from the most recent version of OpenGL, only the most modern graphics cards will be able to run your application. This is often why most developers generally target lower versions of OpenGL and optionally enable higher version functionality

## 2.2: Extensions
A graphics developer can still use these new rendering techniques without having to wait for OpenGL to include the functionality in its future versions, simply by checking if the extension is supported by the graphics card

```
if(GL_ARB_extension_name)
{
// Do cool new and modern stuff supported by hardware
}
else
{
// Extension not supported: do it the old way
}
```

## 2.3: State machine
- OpenGL is a large statemachine, each state is called a **OpenGL context**. When using OpenGL, we often change its state by setting some options, manipulating some buffers and then render using the current context
- When working in OpenGL we will come across several state-changing functions that change the context and several state-using functions that perform some operations based on the current state of OpenGL. As long as you keep in mind that OpenGL is basically one large state machine, most of its functionality will make more sense

## 2.4: Objects

- An object in OpenGL is a collection of options that represents a subset of **OpenGL’s state**.
- Visulize an object as a C-like struct:
```
struct object_name {
  float option1;
  int option2;
  char[] name;
  };
```

- Whenever we want to use objects it generally looks something like this (with OpenGL’s context visualized as a large struct
```
// The State of OpenGL
struct OpenGL_Context {
  ...
  object_name* object_Window_Target;
  ...
};
```

- This little piece of code is a workflow you’ll frequently see when working with OpenGL. We first create an object and store a reference to it as an id (the real object’s data is stored behind the scenes). Then we bind the object (using its id) to the target location of the context (the location of the example window object target is defined as GL_WINDOW_TARGET). Next we set the window options and finally we un-bind the object by setting the current object id of the window target to 0. The options we set are stored in the object referenced by objectId and restored as soon as we bind the object back to GL_WINDOW_TARGET.
```
// create object
unsigned int objectId = 0;
glGenObject(1, &objectId);
// bind/assign object to context
glBindObject(GL_WINDOW_TARGET, objectId);
// set options of object currently bound to GL_WINDOW_TARGET
glSetObjectOption(GL_WINDOW_TARGET, GL_OPTION_WINDOW_WIDTH, 800);
glSetObjectOption(GL_WINDOW_TARGET, GL_OPTION_WINDOW_HEIGHT, 600);
// set context target back to default
glBindObject(GL_WINDOW_TARGET, 0);
```

> The code samples provided so far are only approximations of how OpenGL operates; throughout the book you will come across enough actual examples.

## 2.6 Additional Resources
- www.opengl.org/: official website of OpenGL.
• www.opengl.org/registry/: hosts the OpenGL specifications and extensions for all OpenGL versions.
