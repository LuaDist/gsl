

########### next target ###############

set(gslsum_STAT_SRCS
    levin_u.c
    levin_utrunc.c
    work_u.c
    work_utrunc.c)
set(gslsum_STAT_SRCS ${gslsum_STAT_SRCS} PARENT_SCOPE)

add_library(gslsum STATIC EXCLUDE_FROM_ALL ${gslsum_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslsum gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_sum.h DESTINATION ${INSTALL_INC}/gsl)


