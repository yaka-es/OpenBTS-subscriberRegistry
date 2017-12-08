#
# OpenBTS/CMakeLists.txt
#

cmake_minimum_required(VERSION 3.0)

project(OpenBTS)

option(ORTP_NEW_API "New API of libortp" ON)  # FIXME
option(USE_COREDUMPER "Use libcoredumper" ON)  # FIXME
option(USE_UHD "Use UHD transceiver" ON)  # FIXME
option(USE_UHD_3_9 "Use UHD transceiver (>= v3.9)" ON)  # FIXME
option(USE_RAD1 "Use RAD1 transceiver" ON)  # FIXME

enable_testing()

#include(cmake/features.cmake)

#find_package(Boost COMPONENTS system)
#find_library(USB usb-1.0 REQUIRED)
find_library(ZMQ zmq REQUIRED)

add_compile_options(-g)
add_compile_options(-O2)
add_compile_options(-Wall)
add_compile_options(-Werror)
add_compile_options(-Wno-nonnull-compare)
add_compile_options(-pthread)
add_definitions(-DTIMESTAMP_ISO="unknown")
add_definitions(-DREPO_REV="unknown")

add_definitions(-DHAVE_CONFIG_H)
configure_file(config-cmake.h.in config.h)

set(OPENBTS_COMMON_LIBRARIES -rdynamic sqlite3 pthread dl)

include_directories(${PROJECT_SOURCE_DIR})  # required in apps/OpenBTS.cpp
include_directories(${PROJECT_BINARY_DIR})  # required for <config.h>
include_directories(NodeManager/JsonBox-0.4.3/include)  # required for <JsonBox/*.h>

add_library(openbts-sr
	SubscriberRegistry.cpp
)

add_subdirectory(CommonLibs)
add_subdirectory(Globals)
add_subdirectory(NodeManager)
add_subdirectory(apps)

# install(INSTALLATION)
# install(LEGAL)
# install(COPYING)
# install(README.APIs)
# install(README)
