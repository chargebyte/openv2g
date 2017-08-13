#
# Copyright (c) 2017 Michael Heimpold <mhei@heimpold.de>
#

cmake_minimum_required (VERSION 2.8)
project (openv2g C)

set(OPENV2G_MAJOR_VERSION 0)
set(OPENV2G_MINOR_VERSION 9)
set(OPENV2G_PATCH_VERSION 5)
set(VERSION ${OPENV2G_MAJOR_VERSION}.${OPENV2G_MINOR_VERSION}.${OPENV2G_PATCH_VERSION})
set(SOVERSION 1)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/openv2g.pc.cmakein ${CMAKE_CURRENT_BINARY_DIR}/openv2g.pc @ONLY)

include_directories(src/appHandshake src/codec src/din src/iso1 src/iso2 src/transport src/xmldsig)

file(GLOB SRC_FILES src/appHandshake/* src/codec/* src/din/* src/iso1/* src/iso2/* src/transport/* src/xmldsig/*)
add_library(openv2g SHARED ${SRC_FILES})
set_target_properties(openv2g PROPERTIES SOVERSION ${SOVERSION})

install(TARGETS ${PROJECT_NAME} DESTINATION lib)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/openv2g.pc DESTINATION lib/pkgconfig)

file(GLOB HEADERS src/appHandshake/*.h src/codec/*.h src/din/*.h src/iso1/*.h src/iso2/*.h src/transport/*.h src/xmldsig/*.h)
install(FILES ${HEADERS} DESTINATION include/${PROJECT_NAME})
