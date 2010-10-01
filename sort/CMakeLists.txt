

########### next target ###############

set(gslsort_STAT_SRCS
    sort.c
    sortind.c
    sortvec.c
    sortvecind.c
    subset.c
    subsetind.c)
set(gslsort_STAT_SRCS ${gslsort_STAT_SRCS} PARENT_SCOPE)

add_library(gslsort STATIC EXCLUDE_FROM_ALL ${gslsort_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslsort gslpermutation gslvector gslblock gslieeeutils gslerr gsltest gslsys)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_heapsort.h gsl_sort.h gsl_sort_char.h gsl_sort_double.h gsl_sort_float.h gsl_sort_int.h gsl_sort_long.h gsl_sort_long_double.h gsl_sort_short.h gsl_sort_uchar.h gsl_sort_uint.h gsl_sort_ulong.h gsl_sort_ushort.h gsl_sort_vector.h gsl_sort_vector_char.h gsl_sort_vector_double.h gsl_sort_vector_float.h gsl_sort_vector_int.h gsl_sort_vector_long.h gsl_sort_vector_long_double.h gsl_sort_vector_short.h gsl_sort_vector_uchar.h gsl_sort_vector_uint.h gsl_sort_vector_ulong.h gsl_sort_vector_ushort.h DESTINATION ${INSTALL_INC}/gsl)

