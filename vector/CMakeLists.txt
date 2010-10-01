
########### next target ###############

set(gslvector_STAT_SRCS
    init.c
    file.c
    vector.c
    copy.c
    swap.c
    prop.c
    minmax.c
    oper.c
    reim.c
    subvector.c
    view.c
    view.h)
set(gslvector_STAT_SRCS ${gslvector_STAT_SRCS} PARENT_SCOPE)


#add_library(gslvector STATIC EXCLUDE_FROM_ALL ${gslvector_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslvector gslblock gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### next target ###############

set(test_static_SRCS test_static.c)

if(KDE4_BUILD_TESTS)

add_executable(test_static ${test_static_SRCS})

target_link_libraries(test_static gslvector gslblock gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_vector.h gsl_vector_char.h gsl_vector_complex.h gsl_vector_complex_double.h gsl_vector_complex_float.h gsl_vector_complex_long_double.h gsl_vector_double.h gsl_vector_float.h gsl_vector_int.h gsl_vector_long.h gsl_vector_long_double.h gsl_vector_short.h gsl_vector_uchar.h gsl_vector_uint.h gsl_vector_ulong.h gsl_vector_ushort.h DESTINATION ${INSTALL_INC}/gsl)

#clean: test.txt test.dat
