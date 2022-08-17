cmake_minimum_required(VERSION 3.10.2)

project(external-sodium)
include(ExternalProject)

message(STATUS "Preparing external project \"sodium\"")

ExternalProject_add(
    sodium
    URL https://download.libsodium.org/libsodium/releases/libsodium-1.0.18-stable.tar.gz
    PREFIX sodium
    CONFIGURE_COMMAND <SOURCE_DIR>/configure --prefix=${CMAKE_INSTALL_PREFIX}
    BUILD_COMMAND make
    )
