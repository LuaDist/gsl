
########### next target ###############

set(gslmultiroots_STAT_SRCS
    fdjac.c
    fsolver.c
    fdfsolver.c
    convergence.c
    newton.c
    gnewton.c
    dnewton.c
    broyden.c
    hybrid.c
    hybridj.c)
set(gslmultiroots_STAT_SRCS ${gslmultiroots_STAT_SRCS} PARENT_SCOPE)

add_library(gslmultiroots STATIC EXCLUDE_FROM_ALL ${gslmultiroots_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c test_funcs.c test_funcs.h)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslmultiroots gsllinalg gslblas gslcblas gslpermutation gslmatrix gslvector gslblock gslcomplex gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_multiroots.h DESTINATION ${INSTALL_INC}/gsl)


