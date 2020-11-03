# Protobuf/GRPC with CMake Example

This is a basic example of a cmake project using protobuf together with grpc in c++.

### gRPC Reflection
Reflection can be enabled by linking agains `gRPC::grpc++_reflection`, enabling support for the `grpc_cli` tool.

If this project is linked with a static version of the grpc library from vcpkg
the `-Wl,--whole-archive` flag has to be used. (together with `--allow-multiple-definition`). When linking dynamically,
you will want to link the reflection library with `--no-as-needed`.
