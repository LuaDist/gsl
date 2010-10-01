

########### next target ###############

set(gslfit_STAT_SRCS linear.c)
set(gslfit_STAT_SRCS ${gslfit_STAT_SRCS} PARENT_SCOPE)

add_library(gslfit STATIC EXCLUDE_FROM_ALL ${gslfit_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslfit gslieeeutils gslerr gsltest utils gslsys)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_fit.h DESTINATION ${INSTALL_INC}/gsl)
