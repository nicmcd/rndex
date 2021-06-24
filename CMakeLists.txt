cmake_minimum_required(VERSION 3.20)
project(rndex)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

include(FindPkgConfig)

# libprim
pkg_check_modules(libprim REQUIRED IMPORTED_TARGET libprim)
  get_target_property(
  LIBPRIM_INC
  PkgConfig::libprim
  INTERFACE_INCLUDE_DIRECTORIES
)

# librnd
pkg_check_modules(librnd REQUIRED IMPORTED_TARGET librnd)
  get_target_property(
  LIBRND_INC
  PkgConfig::librnd
  INTERFACE_INCLUDE_DIRECTORIES
)

add_executable(
  rndex
  ${PROJECT_SOURCE_DIR}/src/main.cc
  )

target_include_directories(
  rndex
  PUBLIC
  ${PROJECT_SOURCE_DIR}/src
  ${LIBPRIM_INC}
  ${LIBRND_INC}
  )

target_link_libraries(
  rndex
  PkgConfig::libprim
  PkgConfig::librnd
  )

include(GNUInstallDirs)

install(
  TARGETS
  rndex
  )

