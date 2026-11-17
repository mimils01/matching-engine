cmake_minimum_required(VERSION 3.20)
project(matching_engine LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug)
endif()

include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/refs/tags/v1.15.2.zip
)
FetchContent_MakeAvailable(googletest)

enable_testing()

add_executable(engine_tests engine/tests/sanity_test.cpp)
target_compile_options(engine_tests PRIVATE -Wall -Wextra -Wpedantic)
target_link_libraries(engine_tests PRIVATE GTest::gtest_main)

include(GoogleTest)
gtest_discover_tests(engine_tests)