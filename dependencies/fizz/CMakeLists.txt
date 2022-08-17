cmake_minimum_required(VERSION 3.10.2)

project(external-fizz)
include(ExternalProject)

list(APPEND CMAKE_ARGS
    "-DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX}"
    "-DCMAKE_TOOLCHAIN_FILE:PATH=${CMAKE_TOOLCHAIN_FILE}"
    "-DCMAKE_BUILD_TYPE=Release"
    "-DBUILD_SHARED_LIBS=OFF"
    "-DBUILD_TESTS=OFF"
    "-DBUILD_EXAMPLES=OFF"
    )

message(STATUS "Preparing external project \"fizz\" with args:")
foreach(CMAKE_ARG ${CMAKE_ARGS})
    message(STATUS "-- ${CMAKE_ARG}")
endforeach()

ExternalProject_add(
    fizz
    URL https://github.com/facebookincubator/fizz/releases/download/v2022.07.25.00/fizz-v2022.07.25.00.tar.gz
    PREFIX fizz
    CMAKE_ARGS "${CMAKE_ARGS}"
    SOURCE_SUBDIR fizz
    )
