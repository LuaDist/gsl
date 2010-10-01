
########### next target ###############

set(gsllinalg_STAT_SRCS
    multiply.c
    exponential.c
    tridiag.c
    tridiag.h
    lu.c
    luc.c
    hh.c
    qr.c
    qrpt.c
    lq.c
    ptlq.c
    svd.c
    householder.c
    householdercomplex.c
    hessenberg.c
    hesstri.c
    cholesky.c
    choleskyc.c
    symmtd.c
    hermtd.c
    bidiag.c
    balance.c
    balancemat.c)
set(gsllinalg_STAT_SRCS ${gsllinalg_STAT_SRCS} PARENT_SCOPE)

add_library(gsllinalg STATIC EXCLUDE_FROM_ALL ${gsllinalg_STAT_SRCS})

########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gsllinalg gslblas gslcblas gslpermutation gslmatrix gslvector gslblock gslcomplex gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_linalg.h DESTINATION ${INSTALL_INC}/gsl)

