cmake_minimum_required(VERSION 3.12 FATAL_ERROR)

# Define a project.
project(ASIBOT_OPENRAVE_MODELS LANGUAGES NONE)

# Find dependencies.
find_package(YCM 0.11 REQUIRED)
find_package(YARP 3.2 REQUIRED)

# Set some useful variables - paths relative to the installation prefix.
yarp_configure_external_installation(asibot-openrave-models)

# Configure install rule, copy models to the build directory.
yarp_install(DIRECTORY openrave
             DESTINATION ${ASIBOT-OPENRAVE-MODELS_DATA_INSTALL_DIR})

# Store the package in the user registry.
set(CMAKE_EXPORT_PACKAGE_REGISTRY ON)

# Create and install config files.
include(InstallBasicPackageFiles)

install_basic_package_files(ASIBOT_OPENRAVE_MODELS
                            VERSION 0.1.0
                            COMPATIBILITY AnyNewerVersion
                            NO_EXPORT)

# Add uninstall rule.
include(AddUninstallTarget)
