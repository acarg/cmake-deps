cmake_minimum_required(VERSION 3.10.2)

project(external-zstd)
include(ExternalProject)

list(APPEND CMAKE_ARGS
    "-DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX}"
    "-DCMAKE_PREFIX_PATH:PATH=${CMAKE_PREFIX_PATH}"
    "-DCMAKE_TOOLCHAIN_FILE:PATH=${CMAKE_TOOLCHAIN_FILE}"
    "-DCMAKE_BUILD_TYPE=Release"
    "-DBUILD_SHARED_LIBS=OFF"
    "-DBUILD_TESTING=OFF"
    "-DZSTD_BUILD_PROGRAMS=OFF"
    )

message(STATUS "Preparing external project \"zstd\" with args:")
foreach(CMAKE_ARG ${CMAKE_ARGS})
    message(STATUS "-- ${CMAKE_ARG}")
endforeach()

ExternalProject_add(
    zstd
    URL https://github.com/facebook/zstd/releases/download/v1.5.2/zstd-1.5.2.tar.gz
    PREFIX zstd
    CMAKE_ARGS "${CMAKE_ARGS}"
    SOURCE_SUBDIR build/cmake
    )
