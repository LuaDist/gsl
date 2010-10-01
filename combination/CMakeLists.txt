
########### next target ###############

set(gslcombination_STAT_SRCS
    init.c
    file.c
    combination.c
    inline.c)
set(gslcombination_STAT_SRCS ${gslcombination_STAT_SRCS} PARENT_SCOPE)

add_library(gslcombination STATIC EXCLUDE_FROM_ALL ${gslcombination_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslcombination gslvector gslblock gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_combination.h DESTINATION ${INSTALL_INC}/gsl)


