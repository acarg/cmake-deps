cmake_minimum_required(VERSION 3.10.2)

project(external-wangle)
include(ExternalProject)

list(APPEND CMAKE_ARGS
    "-DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX}"
    "-DCMAKE_TOOLCHAIN_FILE:PATH=${CMAKE_TOOLCHAIN_FILE}"
    "-DCMAKE_BUILD_TYPE=Release"
    "-DBUILD_SHARED_LIBS=OFF"
    "-DBUILD_TESTS=OFF"
    "-DBUILD_EXAMPLES=OFF"
    )

message(STATUS "Preparing external project \"wangle\" with args:")
foreach(CMAKE_ARG ${CMAKE_ARGS})
    message(STATUS "-- ${CMAKE_ARG}")
endforeach()

ExternalProject_add(
    wangle
    URL https://github.com/facebook/wangle/releases/download/v2022.07.25.00/wangle-v2022.07.25.00.tar.gz
    PREFIX wangle
    CMAKE_ARGS "${CMAKE_ARGS}"
    SOURCE_SUBDIR wangle
    )
