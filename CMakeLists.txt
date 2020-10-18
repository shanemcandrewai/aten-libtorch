cmake_minimum_required(VERSION 3.10)

project(aten_libtorch)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(PYTORCH_SRC_DIR ../pytorch)
set(LIBTORCH_SRC_DIR ${PYTORCH_SRC_DIR}/build)
set(LIBTORCH_LIB_DIR ${CMAKE_SOURCE_DIR}/${LIBTORCH_SRC_DIR}/lib)
set(LIBTORCH_DLL_DIR ${CMAKE_SOURCE_DIR}/${LIBTORCH_SRC_DIR}/bin)

add_executable(aten_libtorch aten_min.cpp)
target_include_directories(aten_libtorch PUBLIC ${PYTORCH_SRC_DIR})
target_include_directories(aten_libtorch PUBLIC ${PYTORCH_SRC_DIR}/aten/src)
target_include_directories(aten_libtorch PUBLIC ${LIBTORCH_SRC_DIR})
target_include_directories(aten_libtorch PUBLIC ${LIBTORCH_SRC_DIR}/aten/src)

add_library(torch SHARED IMPORTED)
add_library(c10 SHARED IMPORTED)

if(CMAKE_HOST_SYSTEM_NAME STREQUAL "Linux")
  set_target_properties(torch PROPERTIES IMPORTED_LOCATION ${LIBTORCH_LIB_DIR}/libtorch_cpu.so)
  set_target_properties(c10 PROPERTIES IMPORTED_LOCATION ${LIBTORCH_LIB_DIR}/libc10.so)
elseif(CMAKE_HOST_SYSTEM_NAME STREQUAL "Windows")
  set_target_properties(torch PROPERTIES IMPORTED_IMPLIB ${LIBTORCH_LIB_DIR}/torch_cpu.lib)
  set_target_properties(c10 PROPERTIES IMPORTED_IMPLIB ${LIBTORCH_LIB_DIR}/c10.lib)
  set_target_properties(torch PROPERTIES IMPORTED_LOCATION ${LIBTORCH_DLL_DIR}/torch_cpu.dll)
  set_target_properties(c10 PROPERTIES IMPORTED_LOCATION ${LIBTORCH_DLL_DIR}/c10.dll)
endif()
target_link_libraries(aten_libtorch torch c10)
