
########### next target ###############

set(gslqrng_STAT_SRCS
    gsl_qrng.h
    qrng.c
    niederreiter-2.c
    sobol.c
    halton.c
    reversehalton.c
    inline.c)
set(gslqrng_STAT_SRCS ${gslqrng_STAT_SRCS} PARENT_SCOPE)

add_library(gslqrng STATIC EXCLUDE_FROM_ALL ${gslqrng_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslqrng gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_qrng.h DESTINATION ${INSTALL_INC}/gsl)


