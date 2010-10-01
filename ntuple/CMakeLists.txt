
########### next target ###############

set(gslntuple_STAT_SRCS ntuple.c)
set(gslntuple_STAT_SRCS ${gslntuple_STAT_SRCS} PARENT_SCOPE)

add_library(gslntuple STATIC EXCLUDE_FROM_ALL ${gslntuple_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslntuple gslhistogram gslblock gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_ntuple.h DESTINATION ${INSTALL_INC}/gsl)


