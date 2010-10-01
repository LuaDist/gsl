

########### next target ###############

set(gslblas_STAT_SRCS blas.c)
set(gslblas_STAT_SRCS ${gslblas_STAT_SRCS} PARENT_SCOPE)

add_library(gslblas STATIC EXCLUDE_FROM_ALL ${gslblas_STAT_SRCS})


########### install files ###############

install(FILES  gsl_blas.h gsl_blas_types.h DESTINATION ${INSTALL_INC}/gsl)
