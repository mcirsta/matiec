cmake_minimum_required(VERSION 3.10)

# Set the project name
project(ST2C VERSION 1.0 LANGUAGES CXX)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Include subdirectories
add_subdirectory(absyntax)
add_subdirectory(absyntax_utils)
add_subdirectory(stage1_2)
add_subdirectory(stage3)
add_subdirectory(stage4)

add_executable(st2c main.cc)

target_link_libraries(st2c PRIVATE stage1_2 stage3 stage4_c absyntax absyntax_utils)
