cmake_minimum_required(VERSION 3.22)

project(hello)

add_executable(hello main.cpp)

# add a sub directory in build folder and run CMakeLists.txt in this folder.
# Like processing a new package.
# Better always run it when the package has its own CMakeLists.txt
add_subdirectory(Adder)
# add_library(adder Adder/adder.cpp)

# link directories. However, it can only apply to targets, so you have to add_library first
# target_link_directories(hello PUBLIC Adder) # not very useful
link_directories(Adder) # search for libraries, .so (shared library) or .a (static library) in build folder
include_directories(Adder) # search for include files, headers etc.

add_subdirectory(external/glfw)
# In terminal, use "cmake -DGLFW_BUILD_DOCS=OFF .." to change options

# integrated code
link_directories(
    PRIVATE Adder
    PRIVATE external/glfw/src
)

include_directories(
    PUBLIC Adder
    PUBLIC external/glfw/include
)

target_link_libraries(hello adder glfw)