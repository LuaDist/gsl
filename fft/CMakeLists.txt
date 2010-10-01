
########### next target ###############

set(gslfft_STAT_SRCS dft.c fft.c)
set(gslfft_STAT_SRCS ${gslfft_STAT_SRCS} PARENT_SCOPE)

add_library(gslfft STATIC EXCLUDE_FROM_ALL ${gslfft_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c signals.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslfft gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_fft.h gsl_fft_complex.h gsl_fft_halfcomplex.h gsl_fft_real.h gsl_dft_complex.h gsl_dft_complex_float.h gsl_fft_complex_float.h gsl_fft_halfcomplex_float.h gsl_fft_real_float.h DESTINATION ${INSTALL_INC}/gsl)


