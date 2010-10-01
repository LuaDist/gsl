

########### next target ###############

set(gslmin_STAT_SRCS
    fsolver.c
    golden.c
    brent.c
    convergence.c
    bracketing.c
    quad_golden.c)
set(gslmin_STAT_SRCS ${gslmin_STAT_SRCS} PARENT_SCOPE)

add_library(gslmin STATIC EXCLUDE_FROM_ALL ${gslmin_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c test_funcs.c test.h)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslmin gslieeeutils gslerr gsltest utils gslsys)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_min.h DESTINATION ${INSTALL_INC}/gsl)

