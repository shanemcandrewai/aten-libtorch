cmake_minimum_required(VERSION 3.10)

# set the project name
project(aten_libtorch)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(PYTORCH_SRC_DIR ../pytorch)
set(LIBTORCH_SRC_DIR ../build_libtorch/build)

option(DEBUG "will enable debug builds (-g -O0)" ON)

# add the executable
add_executable(aten_min aten_min.cpp)

add_library(libtorch SHARED IMPORTED)
set_target_properties(libtorch PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/${LIBTORCH_SRC_DIR}/lib/libtorch.so)
target_link_libraries(aten_min libtorch)
target_include_directories(aten_min PUBLIC ${PYTORCH_SRC_DIR})
target_include_directories(aten_min PUBLIC ${PYTORCH_SRC_DIR}/aten/src)
target_include_directories(aten_min PUBLIC ${LIBTORCH_SRC_DIR})
target_include_directories(aten_min PUBLIC ${LIBTORCH_SRC_DIR}/aten/src)
