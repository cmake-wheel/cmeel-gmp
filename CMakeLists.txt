cmake_minimum_required(VERSION 3.20)

set(GMP_VERSION 6.2.1)

project(cmeel-gmp VERSION ${GMP_VERSION})

include(ExternalProject)
ExternalProject_Add(
  gmp
  URL "https://gmplib.org/download/gmp/gmp-${GMP_VERSION}.tar.lz"
  DOWNLOAD_EXTRACT_TIMESTAMP OFF
  BUILD_IN_SOURCE ON
  CONFIGURE_COMMAND "./configure" "--prefix=${CMAKE_INSTALL_PREFIX}"
  COMMAND sed -i.bak "/SUBDIRS/s/ doc//" Makefile
  BUILD_COMMAND "make"
  TEST_COMMAND "make" "check"
  INSTALL_COMMAND "make" "install")

# dummy file for install target
install(FILES README.md DESTINATION share/cmeel-gmp/)
