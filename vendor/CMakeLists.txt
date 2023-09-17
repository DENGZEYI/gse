include(ExternalProject)

MESSAGE(STATUS "building vendor")

set(VENDOR_ROOT ${CMAKE_BINARY_DIR}/vendor)
set(VENDOR_BUILD ${CMAKE_BINARY_DIR}/vendor/vbuild)

# build external project libgse
ExternalProject_Add(LIBGSE
        PREFIX ${VENDOR_ROOT}/libgse
        GIT_REPOSITORY https://github.com/andruxa-smirnov/libgse.git
        GIT_SHALLOW true

        CONFIGURE_COMMAND ./autogen.sh --prefix=${VENDOR_BUILD}
        BUILD_IN_SOURCE true
        BUILD_ALWAYS false

        BUILD_COMMAND make all
        INSTALL_COMMAND make install
        )
add_library(libgse SHARED IMPORTED)
add_dependencies(libgse LIBGSE)
# 因为是使用make编译的文件，所以需要手动指定库文件和头文件的位置
set_target_properties(libgse PROPERTIES
        IMPORTED_LOCATION ${VENDOR_BUILD}/lib/libgse.so
        INTERFACE_INCLUDE_DIRECTORIES ${VENDOR_BUILD}/include)