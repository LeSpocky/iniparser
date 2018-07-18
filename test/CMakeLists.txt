# iniexample
add_executable(iniexample
    iniexample.c
)
target_link_libraries(iniexample
	${PROJECT_NAME}
)
add_test(NAME ${PROJECT_NAME}_iniexample
	COMMAND iniexample
)

# parse
add_executable(parse
    parse.c
)
target_link_libraries(parse
	${PROJECT_NAME}
)
add_test(NAME ${PROJECT_NAME}_parse
	COMMAND parse
	WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)
add_test(NAME ${PROJECT_NAME}_parse_errors
	COMMAND parse twisted-errors.ini
	WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)
add_test(NAME ${PROJECT_NAME}_parse_ofkey
	COMMAND parse twisted-ofkey.ini
	WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)
add_test(NAME ${PROJECT_NAME}_parse_ofval
	COMMAND parse twisted-ofval.ini
	WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)
