cmake_minimum_required(VERSION 3.10.2)

project(external-glog)
include(ExternalProject)

list(APPEND CMAKE_ARGS
    "-DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX}"
    "-DCMAKE_TOOLCHAIN_FILE:PATH=${CMAKE_TOOLCHAIN_FILE}"
    "-DCMAKE_BUILD_TYPE=Release"
    "-DBUILD_SHARED_LIBS=OFF"
    "-DWITH_GTEST=OFF"
    )

message(STATUS "Preparing external project \"glog\" with args:")
foreach(CMAKE_ARG ${CMAKE_ARGS})
    message(STATUS "-- ${CMAKE_ARG}")
endforeach()

ExternalProject_add(
    glog
    URL https://github.com/google/glog/archive/refs/tags/v0.6.0.tar.gz
    PREFIX glog
    CMAKE_ARGS "${CMAKE_ARGS}"
    )
