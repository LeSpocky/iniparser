include(CheckIncludeFile)
check_include_file("stdio.h" HAVE_STDIO_H)
check_include_file("stdlib.h" HAVE_STDLIB_H)
check_include_file("string.h" HAVE_STRING_H)
check_include_file("ctype.h" HAVE_CTYPE_H)
check_include_file("unistd.h" HAVE_UNISTD_H)

set(INIPARSER_SRC
	dictionary.c
	iniparser.c
)

add_library(${PROJECT_NAME} ${INIPARSER_SRC})
add_library(${PROJECT_NAME}::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

set_target_properties(${PROJECT_NAME} PROPERTIES
	OUTPUT_NAME	${PROJECT_NAME}
	SOVERSION	${PROJECT_VERSION_MAJOR}
	VERSION		${PROJECT_VERSION}
	C_STANDARD	99
)

target_include_directories(${PROJECT_NAME}
	PUBLIC
		$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
		$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME}>
)

# taken from upstream Makefile
target_compile_options(${PROJECT_NAME}
	PRIVATE
		"-Wall"
		"-ansi"
		"-pedantic"
)

install(TARGETS ${PROJECT_NAME}
	EXPORT ${PROJECT_NAME}-targets
	LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
	ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
)

install(EXPORT ${PROJECT_NAME}-targets
	NAMESPACE ${PROJECT_NAME}::
	DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}"
)

install(FILES
	dictionary.h
	iniparser.h
	DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME}"
)
