
########### next target ###############

set(gslintegration_STAT_SRCS
    qk15.c
    qk21.c
    qk31.c
    qk41.c
    qk51.c
    qk61.c
    qk.c
    qng.c
    qng.h
    qag.c
    qags.c
    qagp.c
    workspace.c
    qcheb.c
    qawc.c
    qmomo.c
    qaws.c
    qmomof.c
    qawo.c
    qawf.c)
set(gslintegration_STAT_SRCS ${gslintegration_STAT_SRCS} PARENT_SCOPE)

add_library(gslintegration STATIC EXCLUDE_FROM_ALL ${gslintegration_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c tests.c tests.h)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslintegration gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_integration.h DESTINATION ${INSTALL_INC}/gsl)

