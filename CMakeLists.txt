cmake_minimum_required(VERSION 3.22)
include(ExternalProject)

#
# This file is generated only once,
# and is not re-generated if converter is called multiple times.
#
# User is free to modify the file as much as necessary
#

# In order to use CMake for cross-compiling
set(CMAKE_CXX_COMPILER_FORCED "true") 

# Include toolchain file
include("gcc-arm-none-eabi.cmake")

# Set the project name
set(CMAKE_PROJECT_NAME BlinkH7Test2)

# Core project settings
project(${CMAKE_PROJECT_NAME})

# Include external project file
include("mx-generated.cmake")

