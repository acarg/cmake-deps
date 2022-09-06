cmake_minimum_required(VERSION 3.10.2)

project(external-boost)
include(ExternalProject)

message(STATUS "Preparing external project \"boost\"")

if(NOT ${CMAKE_BUILD_TYPE} STREQUAL "Release")
    set(B2_BUILD_TYPE "variant=debug")
else()
    set(B2_BUILD_TYPE "variant=release")
endif()

if(BUILD_SHARED_LIBS)
    set(B2_LINK_TYPE "link=shared")
else()
    set(B2_LINK_TYPE "link=static")
endif()

if(ANDROID)
    if(${CMAKE_ANDROID_ARCH_ABI} STREQUAL "armeabi-v7a")
        set(B2_ARCH "architecture=arm")
        set(B2_ADDRESS_MODEL "address-model=32")
        set(B2_BINARY_FORMAT "binary-format=elf")
        set(B2_ABI "abi=aapcs")
        set(B2_TARGET_OS "target-os=android")
    elseif(${CMAKE_ANDROID_ARCH_ABI} STREQUAL "arm64-v8a")
        set(B2_ARCH "architecture=arm")
        set(B2_ADDRESS_MODEL "address-model=64")
        set(B2_BINARY_FORMAT "binary-format=elf")
        set(B2_ABI "abi=aapcs")
        set(B2_TARGET_OS "target-os=android")
    elseif(${CMAKE_ANDROID_ARCH_ABI} STREQUAL "x86")
        set(B2_ARCH "architecture=x86")
        set(B2_ADDRESS_MODEL "address-model=32")
        set(B2_BINARY_FORMAT "binary-format=elf")
        set(B2_ABI "abi=sysv")
        set(B2_TARGET_OS "target-os=android")
    elseif(${CMAKE_ANDROID_ARCH_ABI} STREQUAL "x86_64")
        set(B2_ARCH "architecture=x86")
        set(B2_ADDRESS_MODEL "address-model=64")
        set(B2_BINARY_FORMAT "binary-format=elf")
        set(B2_ABI "abi=sysv")
        set(B2_TARGET_OS "target-os=android")
    else()
        message(FATAL_ERROR "Unexpected PLATFORM: \"${PLATFORM}\"")
    endif()

    message(STATUS "BUILD_COMMAND: b2 ${B2_ARCH} ${B2_ADDRESS_MODEL} ${B2_BINARY_FORMAT} ${B2_ABI} ${B2_TARGET_OS}")

    ExternalProject_add(
        boost
        URL https://boostorg.jfrog.io/artifactory/main/release/1.80.0/source/boost_1_80_0.tar.gz
        PREFIX boost
        CONFIGURE_COMMAND <SOURCE_DIR>/bootstrap.sh --prefix=${CMAKE_INSTALL_PREFIX}
	BUILD_COMMAND <SOURCE_DIR>/b2 --user-config=${PROJECT_SOURCE_DIR}/dockcross-config.jam --without-python ${B2_ARCH} ${B2_ADDRESS_MODEL} ${B2_BINARY_FORMAT} ${B2_ABI} ${B2_TARGET_OS} ${B2_BUILD_TYPE} ${B2_LINK_TYPE} install
        BUILD_IN_SOURCE TRUE
        INSTALL_COMMAND ""
        )
elseif(MSVC)
    ExternalProject_add(
        boost
        URL https://boostorg.jfrog.io/artifactory/main/release/1.80.0/source/boost_1_80_0.tar.gz
        PREFIX boost
        CONFIGURE_COMMAND <SOURCE_DIR>/bootstrap.bat
        BUILD_COMMAND <SOURCE_DIR>/b2 ${B2_BUILD_TYPE} ${B2_LINK_TYPE} --prefix=${CMAKE_INSTALL_PREFIX} install
        BUILD_IN_SOURCE TRUE
        INSTALL_COMMAND ""
        )
else()
    ExternalProject_add(
        boost
        URL https://boostorg.jfrog.io/artifactory/main/release/1.80.0/source/boost_1_80_0.tar.gz
        PREFIX boost
        CONFIGURE_COMMAND <SOURCE_DIR>/bootstrap.sh --prefix=${CMAKE_INSTALL_PREFIX}
        BUILD_COMMAND <SOURCE_DIR>/b2 ${B2_BUILD_TYPE} ${B2_LINK_TYPE} install
        BUILD_IN_SOURCE TRUE
        INSTALL_COMMAND ""
        )
endif()
