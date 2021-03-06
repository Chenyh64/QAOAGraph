cmake_minimum_required(VERSION 3.0.0)
project(Graph VERSION 0.1.0)

add_library(graph SHARED Graph.cpp)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

include(CTest)
include(FetchContent)
include(GoogleTest)

FetchContent_Declare(
        googletest
        GIT_REPOSITORY https://github.com/google/googletest.git
        GIT_TAG        release-1.11.0
)

FetchContent_GetProperties(googletest)
if(NOT googletest_POPULATED)
        FetchContent_Populate(googletest)
        add_subdirectory(${googletest_SOURCE_DIR} ${googletest_BINARY_DIR})
endif()

option(GRAPH__ENABLE_TESTS "Enable Graph lib tests." ON)

if(GRAPH__ENABLE_TESTS)
        add_subdirectory(test)
endif()
