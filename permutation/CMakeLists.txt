
########### next target ###############

set(gslpermutation_STAT_SRCS
    init.c
    file.c
    permutation.c
    permute.c
    canonical.c
    inline.c)
set(gslpermutation_STAT_SRCS ${gslpermutation_STAT_SRCS} PARENT_SCOPE)

add_library(gslpermutation STATIC EXCLUDE_FROM_ALL ${gslpermutation_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslpermutation gslvector gslblock gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_permutation.h gsl_permute.h gsl_permute_char.h gsl_permute_complex_double.h gsl_permute_complex_float.h gsl_permute_complex_long_double.h gsl_permute_double.h gsl_permute_float.h gsl_permute_int.h gsl_permute_long.h gsl_permute_long_double.h gsl_permute_short.h gsl_permute_uchar.h gsl_permute_uint.h gsl_permute_ulong.h gsl_permute_ushort.h gsl_permute_vector.h gsl_permute_vector_char.h gsl_permute_vector_complex_double.h gsl_permute_vector_complex_float.h gsl_permute_vector_complex_long_double.h gsl_permute_vector_double.h gsl_permute_vector_float.h gsl_permute_vector_int.h gsl_permute_vector_long.h gsl_permute_vector_long_double.h gsl_permute_vector_short.h gsl_permute_vector_uchar.h gsl_permute_vector_uint.h gsl_permute_vector_ulong.h gsl_permute_vector_ushort.h DESTINATION ${INSTALL_INC}/gsl)

