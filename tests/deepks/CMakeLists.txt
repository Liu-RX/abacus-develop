enable_testing()

find_program(BASH bash)
if(ENABLE_ASAN)
    add_test(
        NAME deepks_test_with_asan
        COMMAND ${BASH} ../integrate/Autotest.sh -a ${ABACUS_BIN_PATH} -n 2 -s true
        WORKING_DIRECTORY ${ABACUS_TEST_DIR}/deepks
    )
    add_test(
        NAME deepks_test1_with_asan
        COMMAND ${BASH} Autotest1.sh -a ${CMAKE_CURRENT_BINARY_DIR}/../../source/module_hamilt_lcao/module_deepks/test/test_deepks
        WORKING_DIRECTORY ${ABACUS_TEST_DIR}/deepks
    )

else()
    add_test(
        NAME deepks_test
        COMMAND ${BASH} ../integrate/Autotest.sh -a ${ABACUS_BIN_PATH} -n 4
        WORKING_DIRECTORY ${ABACUS_TEST_DIR}/deepks
    )
    # TODO: I will rewrite the unit tests and remove 604 to module_deepks/test/
    add_test(
       NAME deepks_test1
       COMMAND ${BASH} Autotest1.sh -a ${CMAKE_CURRENT_BINARY_DIR}/../../source/module_hamilt_lcao/module_deepks/test/test_deepks
       WORKING_DIRECTORY ${ABACUS_TEST_DIR}/deepks
    )
endif()
