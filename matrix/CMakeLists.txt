
########### next target ###############

set(gslmatrix_STAT_SRCS
    init.c
    matrix.c
    file.c
    rowcol.c
    swap.c
    copy.c
    minmax.c
    prop.c
    oper.c
    getset.c
    view.c
    submatrix.c
    view.h)
set(gslmatrix_STAT_SRCS ${gslmatrix_STAT_SRCS} PARENT_SCOPE)

add_library(gslmatrix STATIC EXCLUDE_FROM_ALL ${gslmatrix_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslmatrix gslvector gslblock gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### next target ###############

set(test_static_SRCS test_static.c)

if(KDE4_BUILD_TESTS)

add_executable(test_static ${test_static_SRCS})

target_link_libraries(test_static gslmatrix gslvector gslblock gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_matrix.h gsl_matrix_char.h gsl_matrix_complex_double.h gsl_matrix_complex_float.h gsl_matrix_complex_long_double.h gsl_matrix_double.h gsl_matrix_float.h gsl_matrix_int.h gsl_matrix_long.h gsl_matrix_long_double.h gsl_matrix_short.h gsl_matrix_uchar.h gsl_matrix_uint.h gsl_matrix_ulong.h gsl_matrix_ushort.h DESTINATION ${INSTALL_INC}/gsl)



