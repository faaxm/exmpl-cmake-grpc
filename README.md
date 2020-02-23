# Protobuf/GRPC with CMake Example

This is a basic example of a cmake project using protobuf together with grpc in c++.

Reflection is enabled by linking agains `gRPC::grpc++_reflection` enabling support for the `grpc_cli` tool.

This project was linked with a static version of the grpc library from vcpkg and so
the `-Wl,--whole-archive` flag had to be used. (together with `--allow-multiple-definition`). When linking dynamically,
you will want to link the reflection library with `--no-as-needed`.
