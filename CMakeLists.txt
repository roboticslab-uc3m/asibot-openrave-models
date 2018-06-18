cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

# Define a project.
project(ASIBOT_OPENRAVE_MODELS LANGUAGES NONE)

# Find dependencies
find_package(YCM 0.8 REQUIRED)

# https://github.com/roboticslab-uc3m/questions-and-answers/issues/65
find_package(YARP 3.0 QUIET)
if(NOT YARP_FOUND)
    find_package(YARP 2.3.70 REQUIRED)
endif()

# Set some useful variables - paths relative to the installation prefix.
yarp_configure_external_installation(asibot)

# Configure install rule, copy models to the build directory.
yarp_install(DIRECTORY openrave
             DESTINATION ${ASIBOT_CONTEXTS_INSTALL_DIR})

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
file(WRITE ${CMAKE_BINARY_DIR}/${PROJECT_NAME}Config.cmake
     "# Dummy CMake configuration export file.")

# Install CMake configuration file.
install(FILES ${CMAKE_BINARY_DIR}/${PROJECT_NAME}Config.cmake
        DESTINATION ${${PROJECT_NAME}_CMAKE_DESTINATION})

# Add uninstall rule.
include(AddUninstallTarget)
