cmake_minimum_required(VERSION 3.18)

project(rcj-sim)

# use vendor GL libraries if possible
set(OpenGL_GL_PREFERENCE GLVND)

add_subdirectory(libs)

set(CMAKE_CXX_STANDARD 17) # use C++17
set(CMAKE_CXX_STANDARD_REQUIRED ON) # with force
set(CMAKE_CXX_EXTENSIONS OFF) # no GNU extensions

add_subdirectory(mockup)

