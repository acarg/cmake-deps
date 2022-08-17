cmake_minimum_required(VERSION 3.10.2)

project(external-gflags)
include(ExternalProject)

list(APPEND CMAKE_ARGS
    "-DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX}"
    "-DCMAKE_TOOLCHAIN_FILE:PATH=${CMAKE_TOOLCHAIN_FILE}"
    "-DCMAKE_BUILD_TYPE=Release"
    "-DBUILD_SHARED_LIBS=OFF"
    )

message(STATUS "Preparing external project \"gflags\" with args:")
foreach(CMAKE_ARG ${CMAKE_ARGS})
    message(STATUS "-- ${CMAKE_ARG}")
endforeach()

ExternalProject_add(
    gflags
    URL https://github.com/gflags/gflags/archive/refs/tags/v2.2.2.tar.gz
    PREFIX gflags
    CMAKE_ARGS "${CMAKE_ARGS}"
    )
