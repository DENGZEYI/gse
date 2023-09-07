cmake_minimum_required(VERSION 3.0)
project(gse_1 C)

set(CMAKE_C_STANDARD 11)

set(ENV{PKG_CONFIG_PATH} /home/dzy/code/libgse/build_out/lib/pkgconfig)
find_package(PkgConfig)
pkg_search_module(GSE REQUIRED gse)
MESSAGE(STATUS "gse include dirs:" ${GSE_INCLUDE_DIRS})
MESSAGE(STATUS "gse lib:" ${GSE_LIBRARY_DIRS})

include_directories(${GSE_INCLUDE_DIRS})
link_directories(${GSE_LIBRARY_DIRS})


add_executable(test main.c)
#target_include_directories(test PUBLIC ${GSE_INCLUDE_DIRS})
#target_link_libraries(test PUBLIC ${GSE_LIBRARIES})


# application
add_executable(performance ./app/performance.c)
target_link_libraries(performance PUBLIC ${GSE_LIBRARIES})