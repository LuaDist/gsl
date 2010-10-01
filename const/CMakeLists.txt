
########### next target ###############

set(test_SRCS test.c)
set(test_SRCS ${test_SRCS} PARENT_SCOPE)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_const.h gsl_const_cgs.h gsl_const_mks.h gsl_const_cgsm.h gsl_const_mksa.h gsl_const_num.h DESTINATION ${INSTALL_INC}/gsl)


