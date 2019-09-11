project(FAIRSOFT)

cmake_minimum_required(VERSION 3.0)

#enable_testing()

if (IS_DIRECTORY ${CMAKE_SOURCE_DIR}/spack)
  execute_process(COMMAND git pull origin WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}/spack)
else (IS_DIRECTORY ${CMAKE_SOURCE_DIR}/spack)
  execute_process(COMMAND git clone https://github.com/FairRootGroup/spack.git ${CMAKE_SOURCE_DIR}/spack)
endif (IS_DIRECTORY ${CMAKE_SOURCE_DIR}/spack)

set(SPACK_DIR $ENV{SPACK_DIR})
set(FAIRROOT_VERSION $ENV{FAIRROOT_VERSION})
set(SPACK_EXTRA_FLAGS $ENV{SPACK_EXTRA_FLAGS})

configure_file(${CMAKE_SOURCE_DIR}/test/cmaketest.sh.in ${CMAKE_BINARY_DIR}/test/cmaketest.sh)
add_test(NAME build_fairroot_spack COMMAND ${CMAKE_BINARY_DIR}/test/cmaketest.sh)
set_tests_properties(build_fairroot_spack PROPERTIES TIMEOUT 14400)

