
########### next target ###############

set(gslsys_STAT_SRCS
    minmax.c
    prec.c
    hypot.c
    log1p.c
    expm1.c
    coerce.c
    invhyp.c
    pow_int.c
    infnan.c
    fdiv.c
    fcmp.c
    ldfrexp.c)
set(gslsys_STAT_SRCS ${gslsys_STAT_SRCS} PARENT_SCOPE)

add_library(gslsys STATIC EXCLUDE_FROM_ALL ${gslsys_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslsys gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_sys.h DESTINATION ${INSTALL_INC}/gsl)

