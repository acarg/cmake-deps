cmake_minimum_required(VERSION 3.10.2)

project(external-proxygen)
include(ExternalProject)

list(APPEND CMAKE_ARGS
    "-DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX}"
    "-DCMAKE_TOOLCHAIN_FILE:PATH=${CMAKE_TOOLCHAIN_FILE}"
    "-DCMAKE_BUILD_TYPE=Release"
    "-DBUILD_SHARED_LIBS=OFF"
    "-DBUILD_SAMPLES=OFF"
    )

message(STATUS "Preparing external project \"proxygen\" with args:")
foreach(CMAKE_ARG ${CMAKE_ARGS})
    message(STATUS "-- ${CMAKE_ARG}")
endforeach()

ExternalProject_add(
    proxygen
    URL https://github.com/facebook/proxygen/releases/download/v2022.07.25.00/proxygen-v2022.07.25.00.tar.gz
    PREFIX proxygen
    CMAKE_ARGS "${CMAKE_ARGS}"
    )
