cmake_minimum_required(VERSION 2.6)

project(ASIBOT_OPENRAVE_MODELS)

#set(ASIBOT_OPENRAVE_MODELS_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)
#list(APPEND CMAKE_MODULE_PATH ${ASIBOT_OPENRAVE_MODELS_MODULE_PATH})

add_subdirectory(openrave)

configure_file("${CMAKE_SOURCE_DIR}/cmake/template/ASIBOT_OPENRAVE_MODELSConfigUninstall.cmake.in"
               "${CMAKE_BINARY_DIR}/ASIBOT_OPENRAVE_MODELSConfigUninstall.cmake" @ONLY)

add_custom_target(uninstall COMMAND ${CMAKE_COMMAND} -P
                  "${CMAKE_BINARY_DIR}/ASIBOT_OPENRAVE_MODELSConfigUninstall.cmake")
