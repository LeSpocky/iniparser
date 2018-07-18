cmake_minimum_required(VERSION 3.1)

project(iniparser
	VERSION 3.2
	LANGUAGES C
)
message(STATUS "iniparser_VERSION: ${iniparser_VERSION}")

string(TOLOWER ${PROJECT_NAME} PROJECT_NAME_LC)
string(TOUPPER ${PROJECT_NAME} PROJECT_NAME_UC)

# includes
include(CMakePackageConfigHelpers)	# cmake 2.8.8
include(FeatureSummary)
include(GNUInstallDirs)				# cmake 2.8.5

# options
option(BUILD_SHARED_LIBS
    "Global flag to cause add_library to create shared libraries if on."
    ON
)

# add sources
add_subdirectory("src")

# testing
enable_testing()
include(CTest)
add_subdirectory("test")

# cmake package stuff
configure_package_config_file(${PROJECT_NAME_LC}-config.cmake.in
	"${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME_LC}-config.cmake"
	INSTALL_DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}"
	PATH_VARS CMAKE_INSTALL_INCLUDEDIR
	NO_CHECK_REQUIRED_COMPONENTS_MACRO
)
write_basic_package_version_file(
	"${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME_LC}-config-version.cmake"
	VERSION ${PACKAGE_VERSION}
	COMPATIBILITY AnyNewerVersion
)
install(FILES
	${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME_LC}-config.cmake
	${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME_LC}-config-version.cmake
	DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}"
)

# feature summary
message(STATUS "CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}")
feature_summary(WHAT ALL)
