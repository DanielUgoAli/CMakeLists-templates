cmake_minimum_required(VERSION 3.10)
project(MyProject)

set(CMAKE_CXX_STANDARD 17)

include_directories(include)

# Prefer explicit set over glob in production:
#
# set(SOURCES src/model.cc src/data.cc)
# file(GLOB SOURCES "src/*.cc")

add_executable(myexe main.cc ${SOURCES})


if(NOT CMAKE_PREFIX_PATH)
    if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/external/libtorch")
        set(CMAKE_PREFIX_PATH "external/libtorch")
    endif()
endif()
find_package(Torch REQUIRED)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${TORCH_CXX_FLAGS}")

target_link_libraries(myexe "${TORCH_LIBRARIES}")
