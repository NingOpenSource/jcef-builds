# jcef-builds
官网的编译步骤不完整，此处进行补充

原文：[https://bitbucket.org/chromiumembedded/java-cef/wiki/BranchesAndBuilding.md](https://bitbucket.org/chromiumembedded/java-cef/wiki/BranchesAndBuilding.md)

---
## OVERVIEW
CMake is a cross-platform open-source build system that can generate project files in many different formats. It can be downloaded from [http://www.cmake.org](http://www.cmake.org) or installed via a platform package manager.

CMake-generated project formats that have been tested with JCEF include:
```shell
Linux:      Ninja, Unix Makefiles
Mac OS X:   Ninja, Xcode 5+
Windows:    Ninja, Visual Studio 2010+
```
Ninja is a cross-platform open-source tool for running fast builds using pre-installed platform toolchains `(GNU, clang, Xcode or MSVC)`. It can be downloaded from [http://martine.github.io/ninja/](http://martine.github.io/ninja/) or installed via a platform package manager.

## BUILD REQUIREMENTS

The below requirements must be met to build JCEF.
1. `CMake` version 2.8.12.1 or newer.
1. `Linux` requirements: Currently supported distributions include Debian Wheezy, Ubuntu Precise, and related. Ubuntu 14.04 64-bit is recommended. Newer versions will likely also work but may not have been tested.
1.  Required packages include:
    ```shell
    build-essential
    libgtk2.0-dev
    ```
1. `Mac OS X` requirements: `Xcode 5` or newer building on `Mac OS X 10.9 (Mavericks)` or newer. `Xcode 7.2` and `OS X 10.11` are recommended. The `Xcode` command-line tools must also be installed. Only 64-bit builds are supported on OS X.
1.  `Windows` requirements: Visual Studio 2010 or newer building on Windows 7 or newer. Visual Studio 2015 Update 2 and Windows 10 64-bit are recommended.

## BUILD EXAMPLES
The below commands will generate project files and create a Debug build of all JCEF native targets using CMake and the platform toolchain.

Start by creating and entering the CMake build output directory. The `jcef_build` directory name is required by other JCEF tooling (specifically the `tools/make_distrib.[bat|sh]` and `tools/run.[bat|sh]` scripts) and should not be changed.
```shell
> cd path/to/java-cef/src
> mkdir jcef_build && cd jcef_build
```
To perform a `Linux` build using a 32-bit `CEF` binary distribution on a 32-bit `Linux` platform or a 64-bit `CEF` binary distribution on a 64-bit `Linux` platform:

1.  Using `Unix Makefiles`:
    ```shell
    > cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Debug ..
    > make -j4
    ```
  
1.  Using `Ninja`:
    ```shell
    > cmake -G "Ninja" -DCMAKE_BUILD_TYPE=Debug ..
    > ninja
    ```
    
To perform a `Mac OS X` build using a 64-bit `CEF` binary distribution:
1.  Using the `Xcode` IDE:
    ```shell
    > cmake -G "Xcode" -DPROJECT_ARCH="x86_64" ..
    ```
    Open `jcef.xcodeproj` in `Xcode` and select Product > Build.
1.  Using `Unix Makefiles`:
    ```shell
    > cmake -G "Unix Makefiles" -DPROJECT_ARCH="x86_64" -DCMAKE_BUILD_TYPE=Debug ..
    > make -j4
    ```
1.  Using `Ninja`:
    ```shell
    > cmake -G "Ninja" -DPROJECT_ARCH="x86_64" -DCMAKE_BUILD_TYPE=Debug ..
    > ninja
    ```
To perform a `Windows` build using a 32-bit `CEF` binary distribution:
1.  Using the `Visual Studio 2015 IDE`:
    ```shell
    > cmake -G "Visual Studio 14" ..
    ```
    Open `jcef.sln` in `Visual Studio` and select Build > Build Solution.
1.  Using `Ninja` with `Visual Studio 2015` command-line tools:
    ```shell
    (this path may be different depending on your Visual Studio installation)
    > "C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin\vcvars32.bat"
    > cmake -G "Ninja" -DCMAKE_BUILD_TYPE=Debug ..
    > ninja
    ```
To perform a `Windows` build using a 64-bit `CEF` binary distribution:
1.  Using the `Visual Studio 2015 IDE`:
    ```shell
    > cmake -G "Visual Studio 14 Win64" ..
    ```
    Open `jcef.sln` in `Visual Studio` and select Build > Build Solution.
1.  Using `Ninja` with `Visual Studio 2015` command-line tools:
    ```shell
    (this path may be different depending on your Visual Studio installation)
    > "C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\bin\amd64\vcvars64.bat"
    > cmake -G "Ninja" -DCMAKE_BUILD_TYPE=Debug ..
    > ninja
    ```
