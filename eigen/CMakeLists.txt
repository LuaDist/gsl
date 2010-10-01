

########### next target ###############

set(gsleigen_STAT_SRCS
    jacobi.c
    symm.c
    symmv.c
    nonsymm.c
    nonsymmv.c
    herm.c
    hermv.c
    gensymm.c
    gensymmv.c
    genherm.c
    genhermv.c
    gen.c
    genv.c
    sort.c
    francis.c
    schur.c)
set(gsleigen_STAT_SRCS ${gsleigen_STAT_SRCS} PARENT_SCOPE)

add_library(gsleigen STATIC EXCLUDE_FROM_ALL ${gsleigen_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gsleigen gsltest gsllinalg gslpermutation gslblas gslcblas gslmatrix gslvector gslblock gslcomplex gslieeeutils gslsys gslerr utils gslrng gslsort)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_eigen.h DESTINATION ${INSTALL_INC}/gsl)

