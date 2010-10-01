
########### next target ###############

set(gslieeeutils_STAT_SRCS
    print.c
    make_rep.c
    gsl_ieee_utils.h
    env.c
    fp.c
    read.c)
set(gslieee-utils_STAT_SRCS ${gslieeeutils_STAT_SRCS} PARENT_SCOPE)

add_library(gslieeeutils STATIC EXCLUDE_FROM_ALL ${gslieeeutils_STAT_SRCS})

########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_ieee_utils.h DESTINATION ${INSTALL_INC}/gsl)

