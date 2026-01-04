# Hello, Triangle (3D, red)

This small demo renders a single red triangle with distinct z coordinates and a perspective projection so it appears 3D. The window title is "Hello, Triangle".

Dependencies
- CMake >= 3.14
- A C++17 compiler
- GLFW (development headers)
- GLM (headers)
- Internet access (CMake will fetch GLAD automatically via FetchContent)

Install on common systems (examples)

Ubuntu/Debian:
```
sudo apt update
sudo apt install build-essential cmake libglfw3-dev libglm-dev
```

Fedora:
```
sudo dnf install @development-tools cmake glfw-devel glm-devel
```

macOS (with Homebrew):
```
brew install cmake glfw glm
```

Build
```
mkdir build
cd build
cmake ..
cmake --build . --config Release
```

Run
```
./hello_triangle
```

Notes
- If CMake can't find GLFW or GLM on your system, install them via your package manager or build them from source.
- If you prefer to provide GLAD yourself, adjust CMake accordingly; this CMake uses FetchContent to download GLAD automatically at configure time.

Files of interest
- src/main.cpp — main program
- shaders/vertex.glsl — vertex shader
- shaders/fragment.glsl — fragment shader

This program:
- Enables depth testing
- Uses a perspective projection and view transform
- Applies a rotating model matrix to expose the 3D nature of the triangle
- Outputs a pure red color from the fragment shader
