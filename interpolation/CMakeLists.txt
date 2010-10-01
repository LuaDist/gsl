

########### next target ###############

set(gslinterpolation_STAT_SRCS
    accel.c
    akima.c
    cspline.c
    interp.c
    linear.c
    integ_eval.h
    spline.c
    poly.c
    inline.c)
set(gslinterpolation_STAT_SRCS ${gslinterpolation_STAT_SRCS} PARENT_SCOPE)

add_library(gslinterpolation STATIC EXCLUDE_FROM_ALL ${gslinterpolation_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslinterpolation gslpoly gsllinalg gslpermutation gslblas gslmatrix gslvector gslblock gslcomplex gslcblas gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_interp.h gsl_spline.h DESTINATION ${INSTALL_INC}/gsl)

