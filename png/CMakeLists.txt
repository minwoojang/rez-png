CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

include(RezBuild)
include(ExternalProject)

set(png_version ${PNG_VERSION})
#set(url_png http://downloads.sourceforge.net/project/libpng/libpng16/older-releases/${png_version}/libpng-${png_version}.tar.gz)
#set(url_png https://sourceforge.net/project/libpng/libpng16/${png_version}/libpng-${png_version}.tar.gz/download)
set(url_png https://sourceforge.net/projects/libpng/files/libpng16/1.6.44/libpng-1.6.44.tar.gz/download)
#https://sourceforge.net/projects/libpng/files/libpng16/1.6.44/libpng-1.6.44.tar.gz/download

if(${REZ_BUILD_INSTALL})
    set(install_cmd make install ${make_args})
else()
    set(install_cmd "")
endif()

ExternalProject_add(
    png
    URL ${url_png}
    PREFIX png
    CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX} -DCMAKE_POSITION_INDEPENDENT_CODE=ON
    INSTALL_COMMAND "${install_cmd}"
    BUILD_IN_SOURCE 0
)

install(
    FILES cmake/png.cmake
    DESTINATION cmake
)
