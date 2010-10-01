

########### next target ###############

set(gslpoly_STAT_SRCS
    dd.c
    eval.c
    solve_quadratic.c
    solve_cubic.c
    zsolve_quadratic.c
    zsolve_cubic.c
    zsolve.c
    zsolve_init.c
    deriv.c)
set(gslpoly_STAT_SRCS ${gslpoly_STAT_SRCS} PARENT_SCOPE)

add_library(gslpoly STATIC EXCLUDE_FROM_ALL ${gslpoly_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslpoly gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_poly.h DESTINATION ${INSTALL_INC}/gsl)
