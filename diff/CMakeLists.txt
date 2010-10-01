
########### next target ###############

set(gsldiff_STAT_SRCS diff.c)
set(gsldiff_STAT_SRCS ${gsldiff_STAT_SRCS} PARENT_SCOPE)

add_library(gsldiff STATIC EXCLUDE_FROM_ALL ${gsldiff_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gsldiff gslvector gslblock gslieeeutils gslerr gsltest gslsys)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_diff.h DESTINATION ${INSTALL_INC}/gsl)
