cmake_minimum_required(VERSION 2.8)
project( video_udp )
add_executable( video_udp video_udp.cpp )

set(PKG_CONFIG_USE_CMAKE_PREFIX_PATH ON)
find_package(PkgConfig REQUIRED)
if ( NOT (PKGCONFIG_FOUND))
      message(FATAL_ERROR "Please Install PPkgConfig: CMake will Exit")
endif()
pkg_check_modules(GST REQUIRED gstreamer-1.0>=1.8)
if ( NOT (GST_FOUND))
      message(FATAL_ERROR "Please Install Gstreamer Dev: CMake will Exit")
endif()
set(ENV{PKG_CONFIG_PATH})

include_directories("${GST_INCLUDE_DIRS}")

link_libraries(${GST_LIBRARIES})


find_package( OpenCV REQUIRED )
include_directories( ${OpenCV_INCLUDE_DIRS})
target_link_libraries( video_udp ${OpenCV_LIBS} ${GSTREAMER_LIBRARIES})
