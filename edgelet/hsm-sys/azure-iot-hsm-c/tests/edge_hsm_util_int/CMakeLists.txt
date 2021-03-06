#Copyright (c) Microsoft. All rights reserved.
#Licensed under the MIT license. See LICENSE file in the project root for full license information.

#this is CMakeLists.txt for edge_hsm_util_int
cmake_minimum_required(VERSION 2.8.11)

compileAsC11()

include_directories(../../src)

set(theseTestsName edge_hsm_util_int)

add_definitions(-DGB_DEBUG_ALLOC)

prepare_edge_homedir(${theseTestsName})

set(${theseTestsName}_test_files
    ../../src/hsm_utils.c
    ../../src/hsm_log.c
    ${theseTestsName}.c
)

set(${theseTestsName}_h_files

)

build_c_test_artifacts(${theseTestsName} ON "tests/azure_c_shared_utility_tests")

if(WIN32)
    target_link_libraries(${theseTestsName}_exe iothsm aziotsharedutil $ENV{OPENSSL_ROOT_DIR}/lib/ssleay32.lib $ENV{OPENSSL_ROOT_DIR}/lib/libeay32.lib)
else()
     target_link_libraries(${theseTestsName}_exe iothsm aziotsharedutil ${OPENSSL_LIBRARIES})
endif(WIN32)
