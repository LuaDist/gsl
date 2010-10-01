

########### next target ###############

set(gslmonte_STAT_SRCS
    miser.c
    plain.c
    gsl_monte_vegas.h
    gsl_monte_miser.h
    gsl_monte_plain.h
    gsl_monte.h
    vegas.c)
set(gslmonte_STAT_SRCS ${gslmonte_STAT_SRCS} PARENT_SCOPE)

add_library(gslmonte STATIC EXCLUDE_FROM_ALL ${gslmonte_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslmonte gslrng gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_monte.h gsl_monte_vegas.h gsl_monte_miser.h gsl_monte_plain.h DESTINATION ${INSTALL_INC}/gsl)


