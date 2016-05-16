project(game.libretro.dinothawr)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(Kodi REQUIRED)

include(ExternalProject)

if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(LIBRETRO_DEBUG DEBUG=1)
endif()

if("${CORE_SYSTEM_NAME}" STREQUAL "windows")
  set(BUILD_COMMAND mingw32-make platform=win ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "linux")
  set(BUILD_COMMAND make ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "darwin")
  set(BUILD_COMMAND make platform=osx ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "ios")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "android")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "rbpi")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "freebsd")
# TODO
endif()

externalproject_add(dinothawr
                    GIT_REPOSITORY https://github.com/libretro/Dinothawr
                    GIT_TAG cf90f3b
                    PREFIX dinothawr
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND ${BUILD_COMMAND}
                    BUILD_IN_SOURCE 1)

set(DINOTHAWR_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/dinothawr/src/dinothawr/dinothawr_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                            game.libretro.dinothawr${CMAKE_SHARED_LIBRARY_SUFFIX} dinothawr)

build_addon(game.libretro.dinothawr DINOTHAWR DEPLIBS)
add_dependencies(game.libretro.dinothawr dinothawr)

include(CPack)
