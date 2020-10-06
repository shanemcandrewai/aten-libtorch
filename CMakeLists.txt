cmake_minimum_required(VERSION 3.10)

project(aten_libtorch)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_BUILD_TYPE "Debug")

set(PYTORCH_SRC_DIR ../pytorch)
set(LIBTORCH_SRC_DIR ../build_libtorch/build)

add_executable(aten_min aten_min.cpp)
target_include_directories(aten_min PUBLIC ${PYTORCH_SRC_DIR})
target_include_directories(aten_min PUBLIC ${PYTORCH_SRC_DIR}/aten/src)
target_include_directories(aten_min PUBLIC ${LIBTORCH_SRC_DIR})
target_include_directories(aten_min PUBLIC ${LIBTORCH_SRC_DIR}/aten/src)

add_library(torch SHARED IMPORTED)
add_library(c10 SHARED IMPORTED)
set_target_properties(torch PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/${LIBTORCH_SRC_DIR}/lib/libtorch_cpu.so)
set_target_properties(c10 PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/${LIBTORCH_SRC_DIR}/lib/libc10.so)
target_link_libraries(aten_min torch c10)
