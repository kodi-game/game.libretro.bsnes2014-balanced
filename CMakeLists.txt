cmake_minimum_required(VERSION 3.5)
project(game.libretro.bsnes2014-balanced)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

find_package(Kodi REQUIRED)

# CMake on windows only searches for .lib libraries (static library or import library).
# The libretro game library is dynamically loaded so even if an import library would exists it's of no use.
if(CMAKE_SYSTEM_NAME STREQUAL Windows)
  set(_CMAKE_FIND_LIBRARY_SUFFIXES ${CMAKE_FIND_LIBRARY_SUFFIXES})
  set(CMAKE_FIND_LIBRARY_SUFFIXES ${CMAKE_SHARED_LIBRARY_SUFFIX})
endif()
find_library(BSNES2014-BALANCED_LIB NAMES bsnes2014_balanced_libretro${CMAKE_SHARED_LIBRARY_SUFFIX} PATH_SUFFIXES libretro)
if(CMAKE_SYSTEM_NAME STREQUAL Windows)
  set(CMAKE_FIND_LIBRARY_SUFFIXES ${_CMAKE_FIND_LIBRARY_SUFFIXES})
endif()

set(BSNES2014-BALANCED_CUSTOM_BINARY ${BSNES2014-BALANCED_LIB}
    ${PROJECT_NAME}${CMAKE_SHARED_LIBRARY_SUFFIX})

build_addon(${PROJECT_NAME} BSNES2014-BALANCED "")

include(CPack)
