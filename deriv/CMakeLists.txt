
########### next target ###############

set(gslderiv_STAT_SRCS deriv.c)
set(gslderiv_STAT_SRCS ${gslderiv_STAT_SRCS} PARENT_SCOPE)

add_library(gslderiv STATIC EXCLUDE_FROM_ALL ${gslderiv_STAT_SRCS})

########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslderiv gslvector gslblock gslieeeutils gslerr gsltest gslsys)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_deriv.h DESTINATION ${INSTALL_INC}/gsl)

