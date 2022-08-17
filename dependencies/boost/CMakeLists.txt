cmake_minimum_required(VERSION 3.10.2)

project(external-boost)
include(ExternalProject)

message(STATUS "Preparing external project \"boost\"")

ExternalProject_add(
    boost
    URL https://boostorg.jfrog.io/artifactory/main/release/1.80.0/source/boost_1_80_0.tar.gz
    PREFIX boost
    CONFIGURE_COMMAND <SOURCE_DIR>/bootstrap.sh --prefix=${CMAKE_INSTALL_PREFIX}
    BUILD_COMMAND <SOURCE_DIR>/b2
    BUILD_IN_SOURCE TRUE
    INSTALL_COMMAND <SOURCE_DIR>/b2 install
    )
