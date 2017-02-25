cmake_minimum_required(VERSION 2.8.9)

project(AsibotOpenRAVEModels)

find_package(YARP REQUIRED)

list(APPEND CMAKE_MODULE_PATH ${YARP_MODULE_PATH})

include(YarpInstallationHelpers)

yarp_configure_external_installation(asibot)

set(models_dir openrave)
yarp_install(DIRECTORY ${models_dir} DESTINATION ${ASIBOT_CONTEXTS_INSTALL_DIR})

export(PACKAGE ${PROJECT_NAME})

include(CMakePackageConfigHelpers)
include(GNUInstallDirs)

if(WIN32)
    set(ASIBOT_MODELS_CMAKE_DESTINATION "cmake")
else()
    set(ASIBOT_MODELS_CMAKE_DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}")
endif()

set(ASIBOT_MODELS_CONTEXTS_INSTALL_DIR "${ASIBOT_CONTEXTS_INSTALL_DIR}/${models_dir}")

configure_package_config_file("${CMAKE_SOURCE_DIR}/cmake/template/AsibotOpenRAVEModelsConfig.cmake.in"
                              "${CMAKE_BINARY_DIR}/AsibotOpenRAVEModelsConfig.cmake"
                              INSTALL_DESTINATION "${CMAKE_BINARY_DIR}"
                              INSTALL_PREFIX "${CMAKE_BINARY_DIR}"
                              PATH_VARS ASIBOT_MODELS_CONTEXTS_INSTALL_DIR
                              NO_CHECK_REQUIRED_COMPONENTS_MACRO)

configure_package_config_file("${CMAKE_SOURCE_DIR}/cmake/template/AsibotOpenRAVEModelsConfig.cmake.in"
                              "${CMAKE_BINARY_DIR}/AsibotOpenRAVEModelsConfigForInstall.cmake"
                              INSTALL_DESTINATION "${ASIBOT_MODELS_CMAKE_DESTINATION}"
                              PATH_VARS ASIBOT_MODELS_CONTEXTS_INSTALL_DIR
                              NO_CHECK_REQUIRED_COMPONENTS_MACRO)

install(FILES "${CMAKE_BINARY_DIR}/AsibotOpenRAVEModelsConfigForInstall.cmake"
        RENAME AsibotOpenRAVEModelsConfig.cmake
        DESTINATION "${ASIBOT_MODELS_CMAKE_DESTINATION}")

configure_file("${CMAKE_SOURCE_DIR}/cmake/template/AsibotOpenRAVEModelsConfigUninstall.cmake.in"
               "${CMAKE_BINARY_DIR}/AsibotOpenRAVEModelsConfigUninstall.cmake" @ONLY)

add_custom_target(uninstall COMMAND ${CMAKE_COMMAND} -P
                  "${CMAKE_BINARY_DIR}/AsibotOpenRAVEModelsConfigUninstall.cmake")

