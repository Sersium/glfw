# GLFW - Wayland Support Fork

**⚠️ This is a fork of [LWJGL-CI/glfw](https://github.com/LWJGL-CI/glfw), which is itself a fork of the [official GLFW repository](https://github.com/glfw/glfw).**

This fork is maintained for building and testing Wayland support enhancements for GLFW. The CI/CD pipeline has been customized to build GLFW targeting **Linux x64 with Wayland support enabled** using GitHub Actions, without external cloud services or AWS dependencies.

## About GLFW

GLFW is an Open Source, multi-platform library for OpenGL, OpenGL ES and Vulkan application development. It provides a simple, platform-independent API for creating windows, contexts and surfaces, reading input, handling events, etc.

GLFW is written primarily in C99, with parts of macOS support being written in Objective-C.

On Linux, **GLFW supports both Wayland and X11 backends**. This fork emphasizes Wayland support for modern display server environments.

GLFW is licensed under the [zlib/libpng license](https://www.glfw.org/license.html).

For the official GLFW project, visit [glfw.org](https://www.glfw.org/).

## Changelog since 3.4

- Added `GLFW_UNLIMITED_MOUSE_BUTTONS` input mode that allows mouse buttons beyond
   the limit of the mouse button tokens to be reported (#2423)
- Added `glfwGetEGLConfig` function to query the `EGLConfig` of a window (#2045)
- Added `glfwGetGLXFBConfig` function to query the `GLXFBConfig` of a window (#1925)
- Updated minimum CMake version to 3.16 (#2541)
- Removed support for building with original MinGW (#2540)
- [Win32] Removed support for Windows XP and Vista (#2505)
- [Cocoa] Added `QuartzCore` framework as link-time dependency
- [Cocoa] Removed support for OS X 10.10 Yosemite and earlier (#2506)
- [Wayland] Added window icon support via `glfwSetWindowIcon` (#2686)
- [Wayland] Bugfix: The fractional scaling related objects were not destroyed
- [Wayland] Bugfix: `glfwInit` would segfault on compositor with no seat (#2517)
- [Wayland] Bugfix: A drag entering a non-GLFW surface could cause a segfault
- [Wayland] Bugfix: Ignore key repeat events when no window has keyboard focus (#2727)
- [Wayland] Bugfix: Reset key repeat timer when window destroyed (#2741,#2727)
- [Wayland] Bugfix: Memory would leak if reading a data offer failed midway
- [Wayland] Bugfix: Retrieved cursor position would be incorrect when hovering over
                     fallback decorations
- [Wayland] Bugfix: Fallback decorations would report scroll events
- [Wayland] Bugfix: Keyboard repeat events halted when any key is released (#2568)
- [Wayland] Bugfix: Fallback decorations would show menu at wrong position
- [Wayland] Bugfix: The cursor was not updated when clicking through from
   a modal to a fallback decoration
- [Wayland] Bugfix: The cursor position was not updated when clicking through
   from a modal to the content area
- [Wayland] Bugfix: free modules at end of terminate function to resolve
   potential segmentation fault (#2744)
- [Wayland] Bugfix: Confining or disabling the cursor could segfault on
   compositors without `pointer-constraints-unstable-v1`
- [X11] Bugfix: Running without a WM could trigger an assert (#2593,#2601,#2631)
- [X11] Bugfix: Occasional crash when an idle display awakes (#2766)
- [X11] Bugfix: Prevent BadWindow when creating small windows with a content scale
   less than 1 (#2754)
- [X11] Bugfix: Clamp width and height to >= 1 to prevent BadValue error and app exit
- [X11] Bugfix: Floating windows silently became non-floating when hidden (#2276)
- [Linux] Bugfix: The header for `ioctl` was only implicitly included (#2778)
- [Null] Added Vulkan 'window' surface creation via `VK_EXT_headless_surface`
- [Null] Added EGL context creation on Mesa via `EGL_MESA_platform_surfaceless`
- [EGL] Allowed native access on Wayland with `GLFW_CONTEXT_CREATION_API` set to
   `GLFW_NATIVE_CONTEXT_API` (#2518)

## Building This Fork

### Linux (Arch Linux / Wayland) - GitHub Actions

This repository is configured to automatically build GLFW for Linux x64 with full Wayland support whenever code is pushed to the `master` branch. The build artifacts are available as GitHub Actions artifacts.

**Build outputs:**

- `libglfw.so` - The compiled GLFW shared library
- Available in the GitHub Actions "Artifacts" section for 30 days

### Local Build Requirements

To build GLFW locally with Wayland support on Arch Linux, install the required dependencies:

```bash
sudo pacman -S cmake gcc libxrandr libxinerama libxcursor libxi libxext libxkbcommon wayland wayland-protocols
```

Then configure and build:

```bash
cmake -B build -DGLFW_BUILD_WAYLAND=ON -DCMAKE_BUILD_TYPE=Release
cmake --build build --parallel
```

## Key Dependencies for Wayland Support

The GitHub Actions CI verifies that the following dependencies are available:

- **cmake** - Build system
- **gcc, g++** - C/C++ compiler
- **libxrandr-dev** - X11 RandR library
- **libxinerama-dev** - X11 Xinerama library
- **libxcursor-dev** - X11 Cursor library
- **libxi-dev** - X11 Input library
- **libxext-dev** - X11 Extensions library
- **libxkbcommon-dev** - XKB keyboard handling
- **libwayland-dev** - Wayland client libraries
- **wayland-protocols** - Wayland protocol definitions

These correspond to the standard GLFW Wayland/X11 build requirements documented in the [official compilation guide](https://www.glfw.org/docs/latest/compile.html).

## Upstream

- **Parent fork:** [LWJGL-CI/glfw](https://github.com/LWJGL-CI/glfw) - LWJGL project's curated GLFW build
- **Original upstream:** [glfw/glfw](https://github.com/glfw/glfw) - Official GLFW repository

For general GLFW usage, documentation, and API reference, visit the [official GLFW documentation](https://www.glfw.org/docs/latest/).

## Contributing

This is a specialized fork. For general GLFW development and feature requests, please contribute to the [official GLFW repository](https://github.com/glfw/glfw).

For issues specific to this Wayland-focused build or CI/CD configuration, feel free to open an issue in this repository.

The `master` branch is the stable integration branch and _should_ always compile
and run on all supported platforms.  Details of a newly added feature,
including the public API, may change until it has been included in a release.

The `latest` branch is equivalent to the [highest numbered](https://semver.org/)
release, although it may not always point to the same commit as the tag for that
release.

The `ci` branch is used to trigger continuous integration jobs for code under
testing and should never be relied on for any purpose.

## Reporting bugs

Bugs are reported to our [issue tracker](https://github.com/glfw/glfw/issues).
Please check the [contribution
guide](https://github.com/glfw/glfw/blob/master/docs/CONTRIBUTING.md) for
information on what to include when reporting a bug.

## Contact

On [glfw.org](https://www.glfw.org/) you can find the latest version of GLFW, as
well as news, documentation and other information about the project.

If you have questions related to the use of GLFW, we have a
[forum](https://discourse.glfw.org/).

If you have a bug to report, a patch to submit or a feature you'd like to
request, please file it in the
[issue tracker](https://github.com/glfw/glfw/issues) on GitHub.

Finally, if you're interested in helping out with the development of GLFW or
porting it to your favorite platform, join us on the forum or GitHub.
