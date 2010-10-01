
########### next target ###############

set(gsldht_STAT_SRCS dht.c)
set(gsldht_STAT_SRCS ${gsldht_STAT_SRCS} PARENT_SCOPE)

add_library(gsldht STATIC EXCLUDE_FROM_ALL ${gsldht_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gsldht gslspecfunc gslcomplex gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_dht.h DESTINATION ${INSTALL_INC}/gsl)

