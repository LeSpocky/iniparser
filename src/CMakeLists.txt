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
set_target_properties(${PROJECT_NAME} PROPERTIES
	OUTPUT_NAME	${PROJECT_NAME}
	SOVERSION	${PACKAGE_MAJOR_VERSION}
	VERSION		${PACKAGE_VERSION}
)

install(TARGETS ${PROJECT_NAME}
	EXPORT ${PROJECT_NAME}-targets
	LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
	ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
)
install(EXPORT ${PROJECT_NAME}-targets
	DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}"
)

install(FILES
	dictionary.h
	iniparser.h
	DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME}"
)
