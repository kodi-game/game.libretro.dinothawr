cmake_minimum_required(VERSION 3.1)
project(game.libretro.dinothawr)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

find_package(Kodi REQUIRED)
find_library(DINOTHAWR_LIB NAMES dinothawr_libretro${CMAKE_SHARED_LIBRARY_SUFFIX} PATH_SUFFIXES libretro)

set(DINOTHAWR_CUSTOM_BINARY ${DINOTHAWR_LIB}
    ${PROJECT_NAME}${CMAKE_SHARED_LIBRARY_SUFFIX})

build_addon(${PROJECT_NAME} DINOTHAWR "")

include(CPack)
