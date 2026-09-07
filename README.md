# 3D Software Renderer

An experimental C++ renderer that transforms and rasterizes 3D geometry on the CPU. Built with SDL2, it explores the mathematics and implementation behind a basic rendering pipeline: camera orientation, perspective projection, triangle coverage, and depth testing.

![A scene rendered by the engine](https://github.com/user-attachments/assets/07e8e063-786f-40e3-ae88-a65d902d581e)

## Implemented features

- Model, view, and perspective transformations.
- A movable camera with keyboard-controlled position and orientation.
- Triangle rasterization with incremental edge calculations.
- A depth buffer for resolving overlapping geometry.
- Colored cube geometry and a generated demonstration scene.
- Text overlays for frame-rate and camera-distance information.

SDL2 supplies windowing, input, and drawing operations; the geometry transformation and triangle rasterization logic live in the project source.

## Build and run

Requirements:

- A C++20 compiler.
- CMake 3.22.1 or newer.
- SDL2 and SDL2_ttf development libraries.

The current build files use GCC/Clang-style flags, and the source includes platform-specific headers. The following is the intended build flow for a compatible environment; additional portability work may be needed on Windows or non-x86 platforms.

```bash
git clone https://github.com/oabdulr/3DEngine.git
cd 3DEngine
cmake -S . -B build
cmake --build build
cd build
./3DEngine
```

Run from the `build` directory because the font loader resolves `../arial.ttf` relative to the working directory. SDL2_ttf must be available to the compiler and linker; dependencies are not downloaded by CMake.

## Controls

- **W / S:** move forward or backward.
- **A / D:** move sideways.
- **Arrow keys:** change the camera's viewing direction.
- **Close the window:** exit.

Movement currently follows keyboard events rather than a time-based movement model.

## Explore the implementation

- [src/main.cpp](src/main.cpp): sample scene and application loop.
- [src/engine/engine.cpp](src/engine/engine.cpp): SDL initialization, event dispatch, object registration, and timing.
- [src/types/game/camera/camera.cpp](src/types/game/camera/camera.cpp): camera transforms, projection, rasterization, and depth testing.
- [src/types/matrix/matrix4x4.h](src/types/matrix/matrix4x4.h): transformation matrices.
- [src/types/game/objects/shapes/cube.h](src/types/game/objects/shapes/cube.h): cube geometry.

## Scope and limitations

This is a graphics learning project, with no commitment to ongoing feature development. It does not provide a complete game engine or editor.

Near-plane handling and vertex-index preservation need improvement. Resource ownership, shutdown order, and timing initialization also need cleanup. Rendering uses individual SDL pixel operations, and text caching has no eviction policy. There are no automated correctness tests or reproducible performance benchmarks yet.
