cmake_minimum_required(VERSION 3.0)
project(GSE_implementation C)

set(CMAKE_C_STANDARD 11)

# build third-party package
include(${CMAKE_SOURCE_DIR}/vendor/CMakeLists.txt)

# helloWorld
add_executable(helloWorld main.c)
target_include_directories(helloWorld PUBLIC ${VENDOR_BUILD}/include)

# application
add_executable(performance ${CMAKE_SOURCE_DIR}/application/performance.c)
target_include_directories(performance PUBLIC ${VENDOR_BUILD}/include)
target_link_libraries(performance libgse)
