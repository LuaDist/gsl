

########### next target ###############

set(gsltest_STAT_SRCS results.c)

add_library(gsltest STATIC EXCLUDE_FROM_ALL ${gsltest_STAT_SRCS})
set(gsltest_STAT_SRCS ${gsltest_STAT_SRCS} PARENT_SCOPE)

########### install files ###############

install(FILES  gsl_test.h DESTINATION ${INSTALL_INC}/gsl)
