
########### next target ###############

set(gslodeiv_STAT_SRCS
    control.c
    cstd.c
    cscal.c
    evolve.c
    step.c
    rk2.c
    rk2imp.c
    rk2simp.c
    rk4.c
    rk4imp.c
    rkf45.c
    rk8pd.c
    rkck.c
    bsimp.c
    gear1.c
    gear2.c)
set(gslode-initval_STAT_SRCS ${gslodeiv_STAT_SRCS} PARENT_SCOPE)

add_library(gslodeiv STATIC EXCLUDE_FROM_ALL ${gslodeiv_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslodeiv gsllinalg gslblas gslcblas gslmatrix gslpermutation gslvector gslblock gslcomplex gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_odeiv.h DESTINATION ${INSTALL_INC}/gsl)

