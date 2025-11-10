# Learn-Open-GL

# Source 
[LearnOpenGL](https://learnopengl.com/Introduction)
EBook: [Ebook - OpenGL](https://learnopengl.com/book/book_pdf.pdf)

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
- [Official website of OpenGL](www.opengl.org/)
- [Hosts the OpenGL specifications and extensions for all OpenGL versions](www.opengl.org/registry/)

# 3: Creating a window
## 3.1 GLFW
- GLFW is a library, written in C, specifically targeted at OpenGL

> We’ll be building all libraries as 64-bit binaries so make sure to get the 64-bit binaries if you’re using their pre-compiled binaries.


## 3.2: Building GLFW

> Compiling the library from the source code guarantees that the resulting library is perfectly tailored for your CPU/OS, a luxury pre-compiled binaries don’t always provide (sometimes, precompiled binaries are not available for your system)

-  The problem with providing source code to the open world however is that not everyone uses the same IDE or build system for developing their application, which means the project/solution files provided may not be compatible with other people’s setup. So people then have to setup their own project/solution with the given .c/.cpp and .h/.hpp files, which is cumbersome. Exactly for those reasons there is a tool called **CMake**.

**CMake**
- CMake is a tool that can generate project/solution files of the user’s choice (e.g. Visual Studio, Code::Blocks, Eclipse) from a collection of source code files using pre-defined CMake scripts. This allows us to generate a Visual Studio 2019 project file from GLFW’s source package which we can use to compile the library. 

**Building GLFW**
- Step 1: Download GLFW source code
  - [Github](https://github.com/glfw/glfw)
  - [Forked ver](https://github.com/NamPhuThuy/GLFW-Library)
- Step 2: Download and install CMake
  - [CMake download](https://cmake.org/download/)
- Step 3: Install Visual Studio Code
- Step 4:
  - Open CMake
  - Choose the _source code folder_ and the _build folder_
  - 

