
########### next target ###############

set(gslcomplex_STAT_SRCS math.c inline.c)
set(gslcomplex_STAT_SRCS ${gslcomplex_STAT_SRCS} PARENT_SCOPE)

add_library(gslcomplex STATIC EXCLUDE_FROM_ALL ${gslcomplex_STAT_SRCS})


########### next target ###############

set(test_SRCS
    test.c
    results.h
    results1.h
    results2.h
    results_real.h)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslcomplex gslerr gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_complex.h gsl_complex_math.h DESTINATION ${INSTALL_INC}/gsl)

