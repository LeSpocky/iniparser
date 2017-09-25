include_directories(
    "${PROJECT_SOURCE_DIR}/src"
)

# iniexample
add_executable(iniexample
    iniexample.c
)
target_link_libraries(iniexample
	${PROJECT_NAME}
)
add_test(iniexample
	iniexample
)

# parse
add_executable(parse
    parse.c
)
target_link_libraries(parse
	${PROJECT_NAME}
)
add_test(NAME parse
	COMMAND parse
	WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)
add_test(NAME parse-errors
	COMMAND parse twisted-errors.ini
	WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)
add_test(NAME parse-ofkey
	COMMAND parse twisted-ofkey.ini
	WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)
add_test(NAME parse-ofval
	COMMAND parse twisted-ofval.ini
	WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)
