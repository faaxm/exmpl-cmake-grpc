[![Build and Test - Fixed Dependencies](https://github.com/faaxm/exmpl-cmake-grpc/actions/workflows/build.yml/badge.svg)](https://github.com/faaxm/exmpl-cmake-grpc/actions/workflows/build.yml)

[![Build and Test - Latest Dependencies](https://github.com/faaxm/exmpl-cmake-grpc/actions/workflows/build-latest-deps.yml/badge.svg)](https://github.com/faaxm/exmpl-cmake-grpc/actions/workflows/build-latest-deps.yml) (might indicate a bug in dependencies)

# Protobuf/GRPC with CMake Example

This is a basic example of a CMake project using Protobuf together with gRPC in C++.

For some background info, have a look at this blog post explaining [how to structure gRPC projects with CMake](https://www.f-ax.de/dev/2020/11/08/grpc-plugin-cmake-support.html).

## Project Dependencies
The following dependencies exist:
- CMake
- gRPC / protobuf

## Building the Project
There are two ways that can be used to build the code of this repository:

### Install dependencies manually
As this project depends on gRPC and protobuf you must install gRPC and protobuf manually in a separate step.
Please refer to the corresponding documentation of gRPC/protobuf to do that.
You can also find an example for installing the dependencies in this project's `.github/workflows` yaml files.
Once you installed all dependencies run the following commands to build the project:
```
cmake -B build
cmake --build build
```

### Install dependencies via CMake FetchContent
If you do not want to install the gRPC dependency on your system, you can also pull it in via CMake FetchContent.
This will also pull protobuf as it is a dependency for gRPC.
With this method you do not need to install gRPC/manually can simply use the following commands to build the project and its dependencies:
```
cmake -B build -DGRPC_FETCHCONTENT=TRUE -DGRPC_VERSION_TAG=v1.48.1 -DgRPC_BUILD_TESTS=OFF
cmake --build build
```

Note: When using this approach, it will probably improve compilation time to use a compile cache like https://ccache.dev/.

### gRPC Reflection
Reflection can be enabled by linking against `gRPC::grpc++_reflection`, enabling support for the `grpc_cli` tool.

If this project is linked with a static version of the grpc library from vcpkg
the `-Wl,--whole-archive` flag has to be used. (together with `--allow-multiple-definition`). When linking dynamically,
you will want to link the reflection library with `--no-as-needed`.
