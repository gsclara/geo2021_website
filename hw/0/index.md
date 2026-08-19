---
layout: assignment
assignment: 0
---

The instructions in this assignment will help you to have a working system to compile C++ files with CGAL and other external libraries. You don't need to do this assignment, but it will avoid you problems later on.

- - - 
* Table of Content
{:toc}
- - - 

### 1. How to install a nice C++ development environment

There are two or three parts to this:

1. a C++ compiler, which you absolutely need and is what converts your C++ source code to an executable file that you can run;
2. an integrated development environment (IDE), which is highly recommended and provides you with a nice text editor for C++ source code and other programming tools, such as debuggers (to find bugs in your code) and profiling tools (to find what makes it slow); and
3. [CMake](https://cmake.org) as a build system, which is also highly recommended and is a layer between the two parts above.

Our recommendation is that you install [CLion](https://www.jetbrains.com/clion/), [CMake](https://tudelft3d.github.io/geogeeks/cpp/cmake/) and [a C++ compiler](https://tudelft3d.github.io/geogeeks/cpp/install/) using the instructions from [geogeeks](https://tudelft3d.github.io/geogeeks/).

If the above tools don't work well for you or you want some IDE alternatives, [Visual Studio](https://visualstudio.microsoft.com/) is the most popular full featured IDE on Windows, [Xcode](https://developer.apple.com/xcode/) is the one on Mac and [Visual Studio Code](https://code.visualstudio.com/) is a nice simpler alternative that runs on Windows, Mac and Linux. Note that Visual Studio and Xcode have their own build systems that do not rely on CMake.

### 2. Test and understand your C++ development environment

After you have installed the tools listed above, you should test your C++ development environment and make sure that it is working correctly.

If you use the recommended tools (CLion, CMake and a C++ compiler), try step 1 of [this CLion tutorial](https://www.jetbrains.com/help/clion/quick-cmake-tutorial.html#new-project). Make sure that your default C++ project builds and runs correctly. If you use a different (no CLion) setup, try creating a C++ project, building it and running it.

By now, you should have two important files in your project: a C++ source code file with a `.cpp` extension and a CMake configuration file named `CMakeLists.txt`.

First, have a look at the `.cpp` file, which will contain some sample C++ code as an example. If you're using a recent version of CLion, the `.cpp` file will also contain some comments (in green) that teach you how to use certain features of CLion. Note that these comments are regular lines of code, which you can see if you click on the pencil icon (Toggle Rendered View).

Then, try to understand what is happenning in the `CMakeLists.txt` using [this page](https://tudelft3d.github.io/geogeeks/cpp/cmake/#making-sense-of-your-cmakeliststxt-file) of geogeeks. Also, read [this page](https://cplusplus.com/doc/tutorial/introduction/) to understand what your compiler is doing when you tell it to build your project.

If you don't know C++ or need a refresher, [this](https://www.cplusplus.com/doc/tutorial/) is a good series of tutorials. Skim the tutorials in the section titled Basics of C++ and the ones on [Control Structures](https://cplusplus.com/doc/tutorial/control/), [Functions](https://cplusplus.com/doc/tutorial/functions/) and [Input/output with files](https://cplusplus.com/doc/tutorial/files/). You don't need to memorise every single C++ feature in them, but knowing what's available will help you know what to look for in the future. Test and modify some of the examples in your own computer.

The same website is also a very good user friendly reference for the C++ standard library data structures, functions and algorithms. For example, if you want to know the member functions of a [`list`](https://www.cplusplus.com/reference/list/list/) or a [`map`](https://www.cplusplus.com/reference/map/map/).

### 3. Installing CGAL and other C++ libraries

Your C++ development environment already comes with the C++ standard library, which contains a lot of functionality. However, there's much, much more that is available in external libraries, which you have to install.

During the course, we will use [CGAL](https://www.cgal.org/), which is a very nice computational geometry library with a lot of features. Unfortunately, it is also a relatively complex library to install and use, so installing it now will help you to get it working already and to understand the process of installing libraries more generally.

The simplest way to install CGAL (and similar libraries) depends on your operating system. See the sections below.

##### 3.1. Windows

In our opinion, there are three good ways to install CGAL. Each have their pros and cons. These are:

1. using `vcpkg`, Microsoft's package manager for C++ libraries;

2. through the [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/), which is a feature of Windows that allows you to run a Linux environment inside Windows 10 or later; or

3. using [`pixi`](https://pixi.prefix.dev/latest/), which is a cross-platform package manager built on conda.

**`vcpkg` advantages**: If you choose to use `vcpkg`, you'll use less disk space on your computer (several GBs), use less memory because you won't need to run a Linux environment at the same time, generally achieve higher performance, and avoid dealing with two different filesystems (Windows and Linux). `vcpkg` is also what you should use if you want to use Visual Studio instead of CLion.

**WSL advantages** If you choose to use WSL, you'll have access to the easier and less error-prone install processes of CGAL (and other libraries) that are available under Linux, be able to use other nice tools that work better on Linux (e.g. SSH or git clients), generally have access to better support/answers from internet communities, and gain valuable (work) experience using Linux. Also, If you want to take GEO5015: Modelling wind and dispersion in urban environments, you'll most likely use WSL anyway.

**pixi advantages** Pixi puts its own versions of libraries within every project, which can avoid you a lot of issues with broken and/or incompatible versions.

For what is worth, we used to recommend the WSL route in previous years, but now `vcpkg` is very good as well and CLion has added `vcpkg` integration. Pixi seems good but we haven't tested extensively yet.

If you want to go the WSL route, [install it](https://tudelft3d.github.io/geogeeks/linux/wsl/) if you don't have it already. If you already have it but have WSL 1, you should really [upgrade to WSL 2](https://learn.microsoft.com/en-us/windows/wsl/install). Similarly, if you have it but have an old distribution of Linux, we advice that you [upgrade](https://askubuntu.com/questions/1428423/upgrade-ubuntu-in-wsl2-from-20-04-to-22-04) to something relatively recent like Ubuntu-24.04 LTS (or 26.04 LTS when available). Then, follow [this tutorial](https://tudelft3d.github.io/geogeeks/cpp/wslclion/). You can skip the GDAL installation, but you should do all of the rest, including the Connect to CLion section.

If you want to go the `vcpkg` route, have a look at [this tutorial](https://tudelft3d.github.io/geogeeks/cpp/vcpkgwindows/) to install `vcpkg` and CGAL. [Here](cgal_vcpkg_install_manual.pdf) is a more detailed tutorial that explains how to link it to CLion step by step.

If you want to go the `pixi` route, have a look at the docs for the [installation](https://pixi.prefix.dev/latest/installation/), [first workspace](https://pixi.prefix.dev/latest/first_workspace/) and [basic usage](https://pixi.prefix.dev/latest/getting_started/). You'll have to modify the `pixi.toml` in your project root to add CGAL and other dependencies like [this](https://github.com/tudelft3d/val3dity/blob/pixi/pixi.toml).


##### 3.2. Mac

The easiest way is to use [Homebrew](https://brew.sh) (recommended), although it's quite easy to use an alternative like [MacPorts](https://www.macports.org), to use [`pixi`](https://pixi.prefix.dev/latest/) (see the Windows instructions above), or to install them manually (follow the Linux or Unix instructions if there are none for Mac).

Once you have installed Homebrew, you can install CGAL by doing:

```
brew install cgal
```

Note that if you're using an Apple Silicon (arm64) Mac, the paths used by Homebrew are: `/opt/homebrew/include` (for headers) and `/opt/homebrew/lib` (for libraries). If you're using an older Intel (x86-64) Mac, the paths used by Homebrew are: `/usr/local/include` (for headers) and `/usr/local/lib` (for libraries). If you're using CLion, these should be found automatically by CMake. However, if you're using Xcode you will have to put these manually in your project settings.

##### 3.3. Linux

Use the package manager of your distribution (eg `apt` in Ubuntu/Debian), use [`pixi`](https://pixi.prefix.dev/latest/) (see the Windows instructions above), or install them manually.

An example to install CGAL with `apt`:

```
sudo apt-get install libcgal-dev
```

Note that you should get the developer versions of C++ libraries (`-dev`), since these will have all the files you need to develop code, not only to run it. Also note that if you have an old distribution, you'll likely also get an old CGAL version through your package manager.

### 4. How to use C++ libraries?

Anything in the C++ standard library will work after including a header in your C++ source code files. For example, if you want to use [`std::cout` and its `<<` operator](https://www.cplusplus.com/reference/ostream/ostream/operator%3C%3C/), you need include `iostream`:

```
#include <iostream> 
```

However, if you need to use an external library (eg CGAL), you will first need to configure some things for it to compile and link correctly. In IDEs (like Visual Studio or Xcode), this is usually done in the GUI. If you use CMake, this is typically done in your `CMakeLists.txt` file by first calling a script that finds the library. An example using CGAL:

```
find_package( CGAL REQUIRED )
```

The `REQUIRED` keyword makes CMake generate an error if CGAL is not found. This is good because knowing that something is broken with CGAL is much better than getting a cryptic error later on!

Then, you will also need to add a few lines in your CMakeLists that link your project with the CGAL library:

```
add_executable( your_project_name your_source_file.cpp )
target_link_libraries( your_project_name CGAL::CGAL )
```

After those steps, adding the required headers in your `.cpp` file will work. For example, try adding this header to your `.cpp` file, building and running your project:

```
#include <CGAL/Exact_predicates_inexact_constructions_kernel.h>
```

Note that if you use certain (more advanced) parts of CGAL, you will need to add more instructions to your `find_package` and `target_link_libraries` lines. There are some examples [here](https://doc.cgal.org/latest/Manual/devman_create_and_use_a_cmakelist.html).

### 5. Testing your C++ with CGAL installation

In order to make sure that everything is working correctly, you should also test your C++ setup together with CGAL.

We recommend that you do this in two steps. First, try one of the simpler CGAL library examples with no external dependencies, like [this one](https://doc.cgal.org/latest/Polygon/index.html#title3).

Then, try a more complex example with external dependencies, such as [this one](https://doc.cgal.org/latest/Polygon/index.html#title8), which requires Qt6. For that particular example, you will need to add more things to your CMakeLists file. See [here](https://doc.cgal.org/latest/Manual/devman_create_and_use_a_cmakelist.html).

### Acknowledgements

The student assistants of different years have helped us a lot to figure out the best way to install things in different environments. In particular, Özge Tufan contributed most of the WSL instructions and Dimitris Mantas documented the method to use `vcpkg` with CLion.

<!-- ### Likely useful software for the course

  - [QGIS](https://qgis.org/): it has a rudimentary 3D viewer that could be useful and all of GDAL is available
  - [GDAL utilities](https://gdal.org/programs/index.html): to process rasters (included with QGIS)
  - [CloudCompare](http://cloudcompare.org/): to view/edit/process point clouds
  - [Blender](https://www.blender.org/) and [BlenderGIS](https://github.com/domlysz/BlenderGIS): to view 3D models and render them beautifully -->

[last updated: 2026-04-21 16:08]