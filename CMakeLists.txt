cmake_minimum_required(VERSION 3.27)
project(interface_lib_test)

add_library(interface_lib_test INTERFACE)

# ref: https://cmake.org/cmake/help/latest/manual/cmake-buildsystem.7.html#interface-libraries
target_sources(interface_lib_test INTERFACE
  FILE_SET HEADERS # useless line
  BASE_DIRS inc # same as target_include_directories
  FILES inc/prod.h # useless line
)

add_library(platform2 INTERFACE)

target_sources(platform2 PUBLIC
  FILE_SET HEADERS
  BASE_DIRS platform2
  FILES platform2/platform.h
)

add_executable(exe1 src/main.c)
target_link_libraries(exe1 platform2 interface_lib_test)
