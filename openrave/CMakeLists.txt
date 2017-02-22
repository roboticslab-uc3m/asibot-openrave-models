set(appname openrave)

find_package(YARP REQUIRED)

list(APPEND CMAKE_MODULE_PATH ${YARP_MODULE_PATH})

include(YarpInstallationHelpers)

yarp_configure_external_installation(asibot)

file(GLOB asibot ${CMAKE_CURRENT_SOURCE_DIR}/asibot/*.xml)
file(GLOB asibot/ivs ${CMAKE_CURRENT_SOURCE_DIR}/asibot/ivs/*.iv)
file(GLOB asibot/wrls ${CMAKE_CURRENT_SOURCE_DIR}/asibot/wrls/*.wrl)

yarp_install(FILES ${asibot}
             DESTINATION ${ASIBOT_CONTEXTS_INSTALL_DIR}/${appname}/models)

yarp_install(FILES ${asibot/ivs}
             DESTINATION ${ASIBOT_CONTEXTS_INSTALL_DIR}/${appname}/models/ivs)

yarp_install(FILES ${asibot/wrls}
             DESTINATION ${ASIBOT_CONTEXTS_INSTALL_DIR}/${appname}/models/wrls)
