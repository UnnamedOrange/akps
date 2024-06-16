# Copyright (c) UnnamedOrange. Licensed under the MIT License.
# See the LICENSE file in the repository root for full license text.

cmake_minimum_required(VERSION 3.22 FATAL_ERROR)
if(CMAKE_SOURCE_DIR STREQUAL CMAKE_BINARY_DIR)
  message(FATAL_ERROR "In-source builds not allowed. Please make a new directory (called a build directory) and run CMake from there.")
endif()

project(akps
  VERSION 0.1.0
  DESCRIPTION "Core library of akps"
  HOMEPAGE_URL "https://github.com/UnnamedOrange/akps"
  LANGUAGES CXX
)

file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS "inc/*")
add_library(${CMAKE_PROJECT_NAME} INTERFACE "${SOURCES}")
target_compile_features(${CMAKE_PROJECT_NAME} INTERFACE cxx_std_20)
target_include_directories(${CMAKE_PROJECT_NAME}
  INTERFACE
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc>"
)
set_target_properties(${CMAKE_PROJECT_NAME} PROPERTIES
  PUBLIC_HEADER
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc>/"
)

add_subdirectory("example/")
