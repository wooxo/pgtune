cmake_minimum_required(VERSION 3.0)

project(wooxo-pgtune NONE)


################################################################################
# version
################################################################################
set(CPACK_PACKAGE_VERSION_MAJOR "0")
set(CPACK_PACKAGE_VERSION_MINOR "9")
set(CPACK_PACKAGE_VERSION_PATCH "4b")
set(CPACK_PACKAGE_VERSION "${CPACK_PACKAGE_VERSION_MAJOR}.${CPACK_PACKAGE_VERSION_MINOR}.${CPACK_PACKAGE_VERSION_PATCH}")


################################################################################
# install
################################################################################
add_custom_target(${PROJECT_NAME})

install(PROGRAMS pgtune ${INSTALL_TARGETS_DEFAULT_ARGS} DESTINATION /usr/bin)
file(GLOB PG_SETTINGS pg_settings-*)
install(FILES ${PG_SETTINGS} ${INSTALL_TARGETS_DEFAULT_ARGS} DESTINATION /usr/share/pgtune)

################################################################################
# packaging
################################################################################
set(CPACK_DEBIAN_PACKAGE_DEPENDS "postgresql, python2.7")
set(CPACK_DEBIAN_PACKAGE_CONFLICTS "pgtune")
set(CPACK_DEBIAN_PACKAGE_SECTION database)

set(CPACK_PACKAGE_NAME ${PROJECT_NAME})
set(CPACK_PACKAGE_CONTACT Wooxo)
set(CPACK_SYSTEM_NAME amd64)
set(CPACK_GENERATOR "DEB")
set(CPACK_PACKAGE_FILE_NAME "${CPACK_PACKAGE_NAME}_${CPACK_PACKAGE_VERSION}_${CPACK_SYSTEM_NAME}")

include(CPack)
