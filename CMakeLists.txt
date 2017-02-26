cmake_minimum_required(VERSION 2.8.9)

# Define a project.
project(AsibotOpenRAVEModels)

# Find YARP and load configuration, fail otherwise.
find_package(YARP REQUIRED)

# Make YARP's modules visible to current CMake file.
list(APPEND CMAKE_MODULE_PATH ${YARP_MODULE_PATH})

# Load yarp_configure_external_installation() and yarp_install().
include(YarpInstallationHelpers)

# Set some useful variables - paths relative to the installation prefix.
yarp_configure_external_installation(asibot)

set(models_dir openrave)

# Configure install rule, copy models to the build directory.
yarp_install(DIRECTORY ${models_dir} DESTINATION ${ASIBOT_CONTEXTS_INSTALL_DIR})

# Store this package in the user registry.
export(PACKAGE ${PROJECT_NAME})

# Load configure_package_config_file().
include(CMakePackageConfigHelpers)

# Define CMAKE_INSTALL_<dir> and CMAKE_INSTALL_FULL_<dir> variables.
include(GNUInstallDirs)

if(WIN32)
    set(ASIBOT_MODELS_CMAKE_DESTINATION "cmake")
else()
    set(ASIBOT_MODELS_CMAKE_DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}")
endif()

set(ASIBOT_MODELS_CONTEXTS_INSTALL_DIR "${ASIBOT_CONTEXTS_INSTALL_DIR}/${models_dir}")

# Configure <project>Config.cmake file (build tree).
configure_package_config_file("${CMAKE_SOURCE_DIR}/cmake/template/AsibotOpenRAVEModelsConfig.cmake.in"
                              "${CMAKE_BINARY_DIR}/AsibotOpenRAVEModelsConfig.cmake"
                              INSTALL_DESTINATION "${CMAKE_BINARY_DIR}"
                              INSTALL_PREFIX "${CMAKE_BINARY_DIR}"
                              PATH_VARS ASIBOT_MODELS_CONTEXTS_INSTALL_DIR
                              NO_CHECK_REQUIRED_COMPONENTS_MACRO)

# Configure <project>Config.cmake file (install tree).
configure_package_config_file("${CMAKE_SOURCE_DIR}/cmake/template/AsibotOpenRAVEModelsConfig.cmake.in"
                              "${CMAKE_BINARY_DIR}/AsibotOpenRAVEModelsConfigForInstall.cmake"
                              INSTALL_DESTINATION "${ASIBOT_MODELS_CMAKE_DESTINATION}"
                              PATH_VARS ASIBOT_MODELS_CONTEXTS_INSTALL_DIR
                              NO_CHECK_REQUIRED_COMPONENTS_MACRO)

# Rename and install <project>Config.cmake file (install tree).
install(FILES "${CMAKE_BINARY_DIR}/AsibotOpenRAVEModelsConfigForInstall.cmake"
        RENAME AsibotOpenRAVEModelsConfig.cmake
        DESTINATION "${ASIBOT_MODELS_CMAKE_DESTINATION}")

# Configure CMake uninstall script.
configure_file("${CMAKE_SOURCE_DIR}/cmake/template/AsibotOpenRAVEModelsConfigUninstall.cmake.in"
               "${CMAKE_BINARY_DIR}/AsibotOpenRAVEModelsConfigUninstall.cmake" @ONLY)

# Add uninstall rule.
add_custom_target(uninstall COMMAND ${CMAKE_COMMAND} -P
                  "${CMAKE_BINARY_DIR}/AsibotOpenRAVEModelsConfigUninstall.cmake")

