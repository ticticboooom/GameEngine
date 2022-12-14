cmake_minimum_required(VERSION 3.15)


set(CMAKE_TOOLCHAIN_FILE "${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake")
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(Potentia VERSION 0.0.1.0 LANGUAGES CXX)


# ENGINE
file(GLOB_RECURSE ENGINE_FILES "potentia/**/*.h" "potentia/**/*.cpp")
add_library(PotentiaEngine ${ENGINE_FILES})
target_include_directories(PotentiaEngine PUBLIC "./potentia/")

# TESTS

file(GLOB_RECURSE TEST_FILES "./potentia-test/*/*.h" "./potentia-test/*/*.cpp")

add_executable(PotentiaTest ${TEST_FILES})
target_link_libraries(PotentiaTest PUBLIC PotentiaEngine)
target_include_directories(PotentiaTest PUBLIC "./")
find_package(GTest CONFIG REQUIRED)
target_link_libraries(PotentiaTest PRIVATE GTest::gmock GTest::gtest GTest::gmock_main GTest::gtest_main)


# SAMPLE

file(GLOB_RECURSE SAMPLE_FILES "sample/*.h" "sample/*.cpp")
add_executable(PotentiaSample WIN32 ${SAMPLE_FILES})
target_link_libraries(PotentiaSample PUBLIC PotentiaEngine)
target_include_directories(PotentiaSample PUBLIC "./")
