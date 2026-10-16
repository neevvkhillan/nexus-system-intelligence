cmake_minimum_required(VERSION 3.16)
project(NEXUS VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

add_executable(nexus src/main.cpp)
if(WIN32)
    target_link_libraries(nexus PRIVATE psapi)
endif()

if(MSVC)
    target_compile_options(nexus PRIVATE /W4)
else()
    target_compile_options(nexus PRIVATE -Wall -Wextra -Wpedantic)
endif()
