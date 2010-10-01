########### next target ###############

set(gslroots_STAT_SRCS
    bisection.c
    brent.c
    falsepos.c
    newton.c
    secant.c
    steffenson.c
    convergence.c
    fsolver.c
    fdfsolver.c)
set(gslroots_STAT_SRCS ${gslroots_STAT_SRCS} PARENT_SCOPE)

add_library(gslroots STATIC EXCLUDE_FROM_ALL ${gslroots_STAT_SRCS})

########### next target ###############

set(test_SRCS test.c test_funcs.c test.h)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslroots gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_roots.h DESTINATION ${INSTALL_INC}/gsl)

