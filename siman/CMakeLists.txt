
########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslsiman gslrng gslieeeutils gslerr gsltest gslsys utils)


endif(KDE4_BUILD_TESTS)

########### next target ###############

set(siman_tsp_SRCS siman_tsp.c)

add_executable(siman_tsp ${siman_tsp_SRCS})

target_link_libraries(siman_tsp gslsiman gslrng gslieeeutils gslerr gslsys utils)

IF(UNIX)
  target_link_libraries(siman_tsp m)  #~ok?
ENDIF(UNIX)



########### next target ###############

set(gslsiman_STAT_SRCS siman.c)
set(gslsiman_STAT_SRCS ${gslsiman_STAT_SRCS} PARENT_SCOPE)


add_library(gslsiman STATIC EXCLUDE_FROM_ALL ${gslsiman_STAT_SRCS})


########### install files ###############

install(FILES  gsl_siman.h DESTINATION ${INSTALL_INC}/gsl)


