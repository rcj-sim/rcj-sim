cmake_minimum_required(VERSION 3.18)

project(rcj-sim)

# use vendor GL libraries if possible
set(OpenGL_GL_PREFERENCE GLVND)

add_subdirectory(libs)

set(CMAKE_CXX_STANDARD 17) # use C++17
set(CMAKE_CXX_STANDARD_REQUIRED ON) # with force
set(CMAKE_CXX_EXTENSIONS OFF) # no GNU extensions

# for our projects, show all warnings
if(MSVC)
	add_compile_options(/W4)
else()
	add_compile_options(-Wall -Wextra -pedantic)
endif()

add_subdirectory(mockup)

