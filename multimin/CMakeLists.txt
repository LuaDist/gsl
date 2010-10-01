

########### next target ###############

set(gslmultimin_STAT_SRCS
    fdfminimizer.c
    steepest_descent.c
    conjugate_fr.c
    conjugate_pr.c
    convergence.c
    diff.c
    vector_bfgs.c
    vector_bfgs2.c
    fminimizer.c
    simplex.c
    simplex2.c)
set(gslmultimin_STAT_SRCS ${gslmultimin_STAT_SRCS} PARENT_SCOPE)

add_library(gslmultimin STATIC EXCLUDE_FROM_ALL ${gslmultimin_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c test_funcs.c test_funcs.h)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslmultimin gslmin gslpoly gslblas gslcblas gsllinalg gslpermutation gslmatrix gslvector gslblock gslcomplex gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_multimin.h DESTINATION ${INSTALL_INC}/gsl)

