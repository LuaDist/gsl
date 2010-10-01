
########### next target ###############

set(gslstatistics_STAT_SRCS
    mean.c
    variance.c
    absdev.c
    skew.c
    kurtosis.c
    lag1.c
    p_variance.c
    minmax.c
    ttest.c
    median.c
    covariance.c
    quantiles.c
    wmean.c
    wvariance.c
    wabsdev.c
    wskew.c
    wkurtosis.c)
set(gslstatistics_STAT_SRCS ${gslstatistics_STAT_SRCS} PARENT_SCOPE)

add_library(gslstatistics STATIC EXCLUDE_FROM_ALL ${gslstatistics_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c test_nist.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslstatistics gslsort gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_statistics.h gsl_statistics_char.h gsl_statistics_double.h gsl_statistics_float.h gsl_statistics_int.h gsl_statistics_long.h gsl_statistics_long_double.h gsl_statistics_short.h gsl_statistics_uchar.h gsl_statistics_uint.h gsl_statistics_ulong.h gsl_statistics_ushort.h DESTINATION ${INSTALL_INC}/gsl)
