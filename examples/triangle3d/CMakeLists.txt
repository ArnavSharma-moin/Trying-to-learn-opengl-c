cmake_minimum_required(VERSION 3.14)
project(hello_triangle_3d LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# FetchContent for GLAD (loader)
include(FetchContent)
FetchContent_Declare(
  glad
  GIT_REPOSITORY https://github.com/Dav1dde/glad.git
  GIT_TAG master
)
FetchContent_MakeAvailable(glad)

# Find GLFW and GLM on the system
find_package(OpenGL REQUIRED)
find_package(PkgConfig REQUIRED)

# Try pkg-config for glfw3
pkg_check_modules(GLFW3 glfw3)
if (GLFW3_FOUND)
  add_library(glfw STATIC IMPORTED)
  set_target_properties(glfw PROPERTIES
    IMPORTED_LOCATION "${GLFW3_LIBDIR}/libglfw.so"
  )
endif()

# Prefer find_package if available
find_package(GLFW3 REQUIRED)

find_package(glm REQUIRED) # many systems provide glm target

add_executable(hello_triangle src/main.cpp)

target_include_directories(hello_triangle PRIVATE
  ${GLFW3_INCLUDE_DIRS}
)

target_link_libraries(hello_triangle PRIVATE
  glad
  GLFW::GLFW
  OpenGL::GL
  glm::glm
)

# Where to look for shader files at runtime
set(SHADERS_DIR "${CMAKE_SOURCE_DIR}/shaders")
message(STATUS "Shaders directory: ${SHADERS_DIR}")
