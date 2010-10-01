
########### next target ###############

set(gslwavelet_STAT_SRCS
    dwt.c
    wavelet.c
    bspline.c
    daubechies.c
    haar.c)
set(gslwavelet_STAT_SRCS ${gslwavelet_STAT_SRCS} PARENT_SCOPE)

add_library(gslwavelet STATIC EXCLUDE_FROM_ALL ${gslwavelet_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslwavelet gslblas gslcblas gslmatrix gslvector gslblock gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_wavelet.h gsl_wavelet2d.h DESTINATION ${INSTALL_INC}/gsl)
