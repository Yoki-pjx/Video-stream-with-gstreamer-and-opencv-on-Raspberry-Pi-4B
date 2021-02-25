cmake_minimum_required(VERSION 2.8)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

project(video_udp)

set(PKG_CONFIG_USE_CMAKE_PREFIX_PATH ON)

find_package(PkgConfig REQUIRED)
if(NOT(PKGCONFIG_FOUND))
      message(FATAL_ERROR "Please Install PkgConfig: CMake will Exit")
endif()
pkg_check_modules(GST
      REQUIRED
      gstreamer-1.0>=1.8
      gstreamer-plugins-base-1.0>=1.8
)
if(NOT(GST_FOUND))
      message(FATAL_ERROR "Please Install Gstreamer Dev: CMake will Exit")
endif()
set(ENV{PKG_CONFIG_PATH})

find_package(OpenCV REQUIRED)
add_executable(video_udp video_udp.cpp )
target_include_directories(video_udp PUBLIC ${OpenCV_INCLUDE_DIRS} ${GST_INCLUDE_DIRS})
target_link_libraries(video_udp ${OpenCV_LIBS} ${GST_LIBRARIES})
