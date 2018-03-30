# CMake Tutorial - Part 2. Environment Variables

CMake has build in defined environment variables that can be used for modifying the behavior of CMake. 

## Writing out the environment variable

Let us look at the `CMakeLists.txt' file that we created part 1. 

```cmake
cmake_minimum_required(VERSION 3.0.0)
project(hello)
add_executable(${PROJECT_NAME} hello.cpp)
```

With the line `project(hello)` we have set the environment variable `PROJECT_NAME`. We can see the effect by printing out the environment variable. 

```cmake
cmake_minimum_required(VERSION 3.0.0)

message("Project Name: ${PROJECT_NAME}")
project(hello)
message("Project Name: ${PROJECT_NAME}")

add_executable(${PROJECT_NAME} hello.cpp)
```

The output will be
```
Project Name:
Project Name: hello
```

## Setting Environment Variables

You can set environment variables using the `set` command. Here we use `set` to set `PROJECT_NAME`.

```cmake
cmake_minimum_required(VERSION 3.0.0)
set(PROJECT_NAME hello)
message("Project Name: ${PROJECT_NAME}")
add_executable(${PROJECT_NAME} hello.cpp)
```

## Other Environment Variables

### CMAKE_SOURCE_DIR

Let us consider the `CMAKE_SOURCE_DIR` environment variable. We can print out the directory where the `CMakeLists.txt` is located.

```cmake
cmake_minimum_required(VERSION 3.0.0)
project(hello)
message(Source Dir: "${CMAKE_SOURCE_DIR}")
add_executable(${PROJECT_NAME} hello.cpp)
```

### EXECUTABLE_OUTPUT_PATH

When we build the project, `hello` is created in the build directory. We can change where hello is created by changing the `EXECUTABLE_OUTPUT_PATH`. 

`CMAKE_BINARY_DIR` is by default the top level of the build directory. 

We want `hello` to be built in the `bin` directory inside the build directory.

```cmake
cmake_minimum_required(VERSION 3.0.0)
project(hello)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
add_executable(${PROJECT_NAME} hello.cpp)
```

More environment variables are in the [useful variables reference](https://cmake.org/Wiki/CMake_Useful_Variables).

### Other Environment Variables

We can obviously define our own environment variables. Of course, CMake will not do anything with them but they can be used as we would use variables for scripts. 

For example, we can make `HELLO_NAME` as an environment variable and set that as the project name.

```cmake
cmake_minimum_required(VERSION 3.0.0)
set(HELLO_NAME hello)
project(${HELLO_NAME})
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
add_executable(${PROJECT_NAME} hello.cpp)
```

## Conclusion

In this tutorial we have described how to use environment variables to modify how CMake behaves.