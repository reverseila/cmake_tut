# 1. Intro to CMake

## Minimal CMakeLists.txt

```cmake
# If the running version of CMake is lower than the 3.22 required version it
will stop processing the project and report an error.
cmake_minimum_required(VERSION 3.22)

# Name and the language for the project (language part is optional)
# documentation: https://cmake.org/cmake/help/latest/command/project.html
project(hello LANGUAGES CXX)

# Provide the name for the final binary and the source related to it
add_executable(hello hello.cpp)
```

## Invoke CMake & build

Generate and build

```sh
# If you are in the source directory
mkd build && cd $_ && cmake .. && make
cmake -S. -Bbuild && make -C build/
cmake -S. -Bbuild -G Ninja && cd build && ninja
```

```
-S <path-to-source>
  Path to root directory of the CMake project to build.


-B <path-to-build>
  Path to directory which CMake will use as the root of build directory.
  If the directory doesn't already exist CMake will make it.


-G <generator-name>
  Specify a build system generator.

  CMake  may  support  multiple native build systems on certain platforms.  A
  generator is responsible for generating a particular build system.  Possible
  generator names are specified in the cmake-generators(7) manual.

  If not specified, CMake checks the CMAKE_GENERATOR environment variable and
  otherwise falls back to a builtin default selection.
```

Once you invoked the command `cmake -H. -Bbuild`, cmake remembers where the
source folder is - so you can rerun cmake on the build tree with

```sh
cmake /path/to/build/folder/
```

```
--build <dir>
  Project binary directory to be built.  This is required (unless a preset is
  specified) and must be firs
```

## Using ccmake (curses) & cmake-gui

Usefull for finding options and settings
