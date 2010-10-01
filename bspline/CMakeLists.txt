

########### next target ###############

set(gslbspline_STAT_SRCS bspline.c)
set(gslbspline_STAT_SRCS ${gslbspline_STAT_SRCS} PARENT_SCOPE)

add_library(gslbspline STATIC EXCLUDE_FROM_ALL ${gslbspline_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslbspline gsllinalg gslpermutation gslblas gslmatrix gslvector gslblock gslcomplex gslcblas gslieeeutils gslerr gsltest gslsys utils gslstatistics)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_bspline.h DESTINATION ${INSTALL_INC}/gsl)

