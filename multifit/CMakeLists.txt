
########### next target ###############

set(gslmultifit_STAT_SRCS
    multilinear.c
    work.c
    lmder.c
    fsolver.c
    fdfsolver.c
    convergence.c
    gradient.c
    covar.c)
set(gslmultifit_STAT_SRCS ${gslmultifit_STAT_SRCS} PARENT_SCOPE)

add_library(gslmultifit STATIC EXCLUDE_FROM_ALL ${gslmultifit_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslmultifit gsllinalg gslpermutation gslblas gslcblas gslmatrix gslvector gslblock gslcomplex gslieeeutils gslerr gsltest utils gslsys)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_multifit.h gsl_multifit_nlin.h DESTINATION ${INSTALL_INC}/gsl)

