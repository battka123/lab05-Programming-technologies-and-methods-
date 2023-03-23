cmake_minimum_required(VERSION 3.4)

SET(COVERAGE OFF CACHE BOOL "Coverage")

SET(CMAKE_CXX_COMPILER "/usr/bin/g++")

project(lab)

#set(CMAKE_CXX_STANDARD 11)

#set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/gtest" "gtest")

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/banking)

add_executable(tests ${CMAKE_CURRENT_SOURCE_DIR}/tests/test.cpp) 

if (COVERAGE) 

target_compile_options(tests PRIVATE --coverage)

target_link_libraries(tests PRIVATE --coverage)
endif()

target_include_directories(tests PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/banking)

target_link_libraries(tests PRIVATE gtest gtest_main gmock_main banking)
