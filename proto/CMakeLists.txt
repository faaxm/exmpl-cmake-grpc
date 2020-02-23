find_package(protobuf CONFIG REQUIRED)
find_package(gRPC CONFIG REQUIRED)

include(protobuf_gen)

set(PROTO_FILES
    myproto/address.proto
    myproto/addressbook.proto
)

get_target_property(grpc_cpp_plugin_file gRPC::grpc_cpp_plugin LOCATION)

add_library(myproto ${PROTO_FILES})
target_link_options(myproto BEFORE INTERFACE -Wl,--allow-multiple-definition)
target_link_libraries(myproto
    PUBLIC
        protobuf::libprotobuf
        gRPC::grpc
        -Wl,--whole-archive gRPC::grpc++_reflection -Wl,--no-whole-archive
)
target_include_directories(myproto PUBLIC ${CMAKE_CURRENT_BINARY_DIR})

my_protobuf_generate(TARGET myproto LANGUAGE cpp)
my_protobuf_generate(TARGET myproto LANGUAGE grpc GENERATE_EXTENSIONS .grpc.pb.h .grpc.pb.cc PLUGIN "protoc-gen-grpc=${grpc_cpp_plugin_file}")
