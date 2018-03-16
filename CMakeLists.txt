cmake_minimum_required(VERSION 2.8.9)

# Define a project.
project(ASIBOT_OPENRAVE_MODELS)

# Load custom CMake modules.
list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)

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

# Define CMAKE_INSTALL_<dir> and CMAKE_INSTALL_FULL_<dir> variables.
include(GNUInstallDirs)

# Set installation path for CMake files.
if(WIN32)
    set(${PROJECT_NAME}_CMAKE_DESTINATION "CMake")
else()
    set(${PROJECT_NAME}_CMAKE_DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}")
endif()

# Create dummy CMake configuration export file.
file(WRITE ${CMAKE_BINARY_DIR}/${PROJECT_NAME}Config.cmake "# Dummy CMake configuration export file.")

# Install CMake configuration file.
install(FILES ${CMAKE_BINARY_DIR}/${PROJECT_NAME}Config.cmake
        DESTINATION ${${PROJECT_NAME}_CMAKE_DESTINATION})

# Add uninstall rule.
include(AddUninstallTarget)
