cmake_minimum_required(VERSION 3.10.2)

project(external-double-conversion)
include(ExternalProject)

list(APPEND CMAKE_ARGS
    "-DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX}"
    "-DCMAKE_PREFIX_PATH:PATH=${CMAKE_PREFIX_PATH}"
    "-DCMAKE_TOOLCHAIN_FILE:PATH=${CMAKE_TOOLCHAIN_FILE}"
    "-DCMAKE_BUILD_TYPE=Release"
    "-DBUILD_SHARED_LIBS=OFF"
    "-DBUILD_TESTING=OFF"
    )

message(STATUS "Preparing external project \"double_conversion\" with args:")
foreach(CMAKE_ARG ${CMAKE_ARGS})
    message(STATUS "-- ${CMAKE_ARG}")
endforeach()

ExternalProject_add(
    double_conversion
    URL https://github.com/google/double-conversion/archive/refs/tags/v3.2.0.tar.gz
    PREFIX double_conversion
    CMAKE_ARGS "${CMAKE_ARGS}"
    )
