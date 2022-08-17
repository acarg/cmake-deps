cmake_minimum_required(VERSION 3.10.2)

project(external-fmt)
include(ExternalProject)

list(APPEND CMAKE_ARGS
    "-DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX}"
    "-DCMAKE_TOOLCHAIN_FILE:PATH=${CMAKE_TOOLCHAIN_FILE}"
    "-DCMAKE_BUILD_TYPE=Release"
    "-DBUILD_SHARED_LIBS=OFF"
    "-DFMT_DOC=OFF"
    "-DFMT_TEST=OFF"
    "-DFMT_FUZZ=OFF"
    "-DFMT_CUDA_TEST=OFF"
    "-DFMT_MODULE=ON"
    )

message(STATUS "Preparing external project \"fmt\" with args:")
foreach(CMAKE_ARG ${CMAKE_ARGS})
    message(STATUS "-- ${CMAKE_ARG}")
endforeach()

ExternalProject_add(
    fmt
    URL https://github.com/fmtlib/fmt/archive/refs/tags/9.0.0.tar.gz
    PREFIX fmt
    CMAKE_ARGS "${CMAKE_ARGS}"
    )
