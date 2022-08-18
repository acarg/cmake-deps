cmake_minimum_required(VERSION 3.10.2)

project(external-folly)
include(ExternalProject)

list(APPEND CMAKE_ARGS
    "-DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX}"
    "-DCMAKE_TOOLCHAIN_FILE:PATH=${CMAKE_TOOLCHAIN_FILE}"
    "-DCMAKE_BUILD_TYPE=Release"
    "-DBUILD_SHARED_LIBS=OFF"
    "-DBUILD_TESTS=OFF"
    "-DBUILD_BENCHMARKS=OFF"
    "-DBUILD_BROKEN_TESTS=OFF"
    "-DBUILD_HANGING_TESTS=OFF"
    "-DBUILD_SLOW_TESTS=OFF"
    )

message(STATUS "Preparing external project \"folly\" with args:")
foreach(CMAKE_ARG ${CMAKE_ARGS})
    message(STATUS "-- ${CMAKE_ARG}")
endforeach()

ExternalProject_add(
    folly
    URL https://github.com/facebook/folly/releases/download/v2022.07.25.00/folly-v2022.07.25.00.tar.gz
    PREFIX folly
    CMAKE_ARGS "${CMAKE_ARGS}"
    )
