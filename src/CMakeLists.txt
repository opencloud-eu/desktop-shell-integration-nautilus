configure_file(syncstate.py syncstate.py COPYONLY)

# Create a nemo plugin script from the nautilus one.
# nemocmd copies the syncstate.py and performs string replacement.
execute_process(
    COMMAND "${CMAKE_CURRENT_SOURCE_DIR}/createnemoplugin.sh" ${CMAKE_CURRENT_SOURCE_DIR}
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    ERROR_VARIABLE errors
    OUTPUT_VARIABLE out
)

# Create a caja plugin script from the nautilus one.
# cajacmd copies the syncstate.py and performs string replacement.
execute_process(
    COMMAND "${CMAKE_CURRENT_SOURCE_DIR}/createcajaplugin.sh" ${CMAKE_CURRENT_SOURCE_DIR}
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    ERROR_VARIABLE errors
    OUTPUT_VARIABLE out
)

install(FILES syncstate.py DESTINATION ${CMAKE_INSTALL_DATADIR}/nautilus-python/extensions RENAME syncstate-OpenCloud.py)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/syncstate_nemo.py DESTINATION ${CMAKE_INSTALL_DATADIR}/nemo-python/extensions RENAME syncstate-OpenCloud.py)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/syncstate_caja.py DESTINATION ${CMAKE_INSTALL_DATADIR}/caja-python/extensions RENAME syncstate-OpenCloud.py)
