# Copyright (c) UnnamedOrange. Licensed under the MIT License.
# See the LICENSE file in the repository root for full license text.

cmake_minimum_required(VERSION 3.22 FATAL_ERROR)
if(CMAKE_SOURCE_DIR STREQUAL CMAKE_BINARY_DIR)
  message(FATAL_ERROR "In-source builds not allowed. Please make a new directory (called a build directory) and run CMake from there.")
endif()

file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS "src/*")
add_executable(akps-example "${SOURCES}")
target_compile_features(akps-example PRIVATE cxx_std_20)
if(MSVC)
  target_compile_options(akps-example PRIVATE /W4 /permissive- /WX)
  target_compile_options(akps-example PRIVATE /utf-8)
  target_compile_definitions(akps-example PRIVATE UNICODE _UNICODE)
else()
  target_compile_options(akps-example PRIVATE -Wall -Wextra -Wpedantic -Werror)
endif()
set_target_properties(akps-example PROPERTIES
  WIN32_EXECUTABLE FALSE
)
target_precompile_headers(akps-example PRIVATE "src/pch.hpp")
target_link_libraries(akps-example PRIVATE
  ${CMAKE_PROJECT_NAME}
)
