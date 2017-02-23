cmake_minimum_required(VERSION 2.6)

project(ASIBOT_OPENRAVE_MODELS)

find_package(YARP REQUIRED)

list(APPEND CMAKE_MODULE_PATH ${YARP_MODULE_PATH})

include(YarpInstallationHelpers)

yarp_configure_external_installation(asibot)

yarp_install(DIRECTORY openrave DESTINATION ${ASIBOT_CONTEXTS_INSTALL_DIR})

configure_file("${CMAKE_SOURCE_DIR}/cmake/template/ASIBOT_OPENRAVE_MODELSConfigUninstall.cmake.in"
               "${CMAKE_BINARY_DIR}/ASIBOT_OPENRAVE_MODELSConfigUninstall.cmake" @ONLY)

add_custom_target(uninstall COMMAND ${CMAKE_COMMAND} -P
                  "${CMAKE_BINARY_DIR}/ASIBOT_OPENRAVE_MODELSConfigUninstall.cmake")

