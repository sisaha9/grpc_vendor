cmake_minimum_required(VERSION 3.10)
project(grpc_vendor CXX)

find_package(ament_cmake REQUIRED)
find_package(ament_cmake_vendor_package REQUIRED)
find_package(protobuf 3.21.12.0 QUIET)
find_package(gRPC 1.54.1 QUIET)

ament_vendor(grpc_vendor
  SATISFIED ${gRPC_FOUND}
  VCS_URL https://github.com/grpc/grpc.git
  VCS_VERSION v1.54.1
  CMAKE_ARGS
    -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE}
    -DgRPC_INSTALL=ON:BOOL=ON
    -DgRPC_BUILD_TESTS:BOOL=OFF
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  list(APPEND AMENT_LINT_AUTO_EXCLUDE
    ament_cmake_cppcheck
  )
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()