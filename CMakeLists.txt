cmake_minimum_required(VERSION 3.5)
include(evmc/cmake/cable/bootstrap.cmake)
include(CableBuildInfo)
include(CableBuildType)
include(CableToolchains)
include(GNUInstallDirs)

if(UNIX)
    # Build deps with PIC to allow building shared libraries.
    set(toolchain cxx11-pic)
else()
    set(toolchain cxx11)
endif()
cable_configure_toolchain(DEFAULT ${toolchain})

# Require C++11.
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_CXX_EXTENSIONS Off)
add_definitions(-DETH_FATDB)
cable_set_build_type(DEFAULT RelWithDebInfo CONFIGURATION_TYPES Debug;Release;RelWithDebInfo)

cable_add_buildinfo_library(PREFIX aleth)

include(EthCompilerSettings)
include(EthOptions)

# add_compile_options(-Wall -Wshorten-64-to-32 -Werror -Wextra -Wconversion -Wno-sign-conversion -Wno-unknown-pragmas)
include_directories(${CMAKE_SOURCE_DIR} ${CMAKE_SOURCE_DIR}/mvm)

add_subdirectory(evmc)
add_subdirectory(evmjit)
add_subdirectory(hera)
add_subdirectory(libevm)
add_subdirectory(libdevcrypto)
add_subdirectory(libethcore)
add_subdirectory(ethash)
add_subdirectory(libmol)
add_subdirectory(libdevcore)
add_subdirectory(libethashseal)
add_subdirectory(aleth-vm)
include_directories (evmc)
include_directories (evmjit)
include_directories (hera)
include_directories (libevm)
include_directories (libdevcrypto)
include_directories (libethcore)
include_directories (libdevcore)
include_directories (libmol)
include_directories (libethashseal)
include_directories (ethash)
include_directories (aleth-vm)


option(ALETH_INTERPRETER_SHARED "Build aleth-interpreter as a shared library" OFF)
add_subdirectory(libaleth-interpreter)

set(UTILS_INCLUDE_DIR "${CMAKE_SOURCE_DIR}/mvm/utils")
message("CMAKE_SOURCE_DIR:"${CMAKE_SOURCE_DIR})
message("UTILS_INCLUDE_DIR:"${UTILS_INCLUDE_DIR})

message("CRYPTOPP_LIBRARY-p:"${CRYPTOPP_LIBRARY})



