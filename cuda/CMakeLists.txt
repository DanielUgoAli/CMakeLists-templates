cmake_minimum_required(VERSION 3.18)  # For CUDA language support
project(MyProject LANGUAGES CXX CUDA)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CUDA_STANDARD 17)
set(CMAKE_CUDA_STANDARD_REQUIRED ON)

include_directories(include)

# Prefer explicit set over glob in production:
#
# set(SOURCES src/kernel.cu src/helper.cc)
# file(GLOB SOURCES "src/*.cc" "src/*.cu")

add_executable(myexe main.cc ${SOURCES})

set_target_properties(myexe PROPERTIES
    CUDA_SEPARABLE_COMPILATION ON
    CUDA_ARCHITECTURES "native"  # Or specify e.g., "75" for RTX 20xx
)

# CUDA libraries are automatically linked when using CUDA language support
# No need for find_package(CUDA) with modern CMake
