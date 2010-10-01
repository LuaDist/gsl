
########### next target ###############

set(gslcheb_STAT_SRCS
    deriv.c
    eval.c
    init.c
    integ.c)
set(gslcheb_STAT_SRCS ${gslcheb_STAT_SRCS} PARENT_SCOPE)

add_library(gslcheb STATIC EXCLUDE_FROM_ALL ${gslcheb_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslcheb gslieeeutils gsltest gslsys gslerr utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_chebyshev.h DESTINATION ${INSTALL_INC}/gsl)


