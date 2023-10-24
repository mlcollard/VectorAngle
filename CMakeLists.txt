# @file CMakeLists.txt
# 
# CMake files for VectorAngle

cmake_minimum_required(VERSION 3.20)

# Project info
project(VectorAngle)

# C++17 standard
set(CMAKE_CXX_STANDARD 17)

# Turn on all warnings, and make warnings errors
if(MSVC)
    add_compile_options(/W4)
else()
    add_compile_options(-Wall -Wextra -pedantic)
endif()

# Main application
add_executable(vector_angle VectorAngle.cpp dotProduct.cpp)
target_compile_features(vector_angle PRIVATE cxx_std_17)

# Run application
add_custom_target(run COMMENT "Run demonstration"
                      COMMAND $<TARGET_FILE:vector_angle>  "1.0,2.0,3.0" "4.0,5.0,6.0"
                      DEPENDS vector_angle)

# Dot product test program
add_executable(dotProductTest dotProductTest.cpp dotProduct.cpp)
target_compile_features(dotProductTest PRIVATE cxx_std_17)

# Run test
add_custom_target(test COMMENT "Run test"
                      COMMAND $<TARGET_FILE:dotProductTest>
                      DEPENDS dotProductTest)
