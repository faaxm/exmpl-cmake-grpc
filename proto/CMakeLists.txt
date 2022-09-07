include(grpc)
find_package(Threads)

#
# Protobuf/Grpc source files
#
set(PROTO_FILES
    myproto/address.proto
    myproto/addressbook.proto
)

#
# Add Library target with protobuf sources
#
add_library(myproto ${PROTO_FILES})
target_link_libraries(myproto
    PUBLIC
        ${_PROTOBUF_LIBPROTOBUF}
	${_GRPC_GRPCPP}
        #gRPC::grpc
)
target_include_directories(myproto PUBLIC ${CMAKE_CURRENT_BINARY_DIR})

#
# Compile protobuf and grpc files in myproto target to cpp
#
protobuf_generate(TARGET myproto LANGUAGE cpp)
protobuf_generate(TARGET myproto LANGUAGE grpc GENERATE_EXTENSIONS .grpc.pb.h .grpc.pb.cc PLUGIN "protoc-gen-grpc=${_GRPC_CPP_PLUGIN_EXECUTABLE}")
