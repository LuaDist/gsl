

########### next target ###############

set(gslerr_STAT_SRCS
    error.c
    stream.c
    message.c
    strerror.c)
set(gslerr_STAT_SRCS ${gslerr_STAT_SRCS} PARENT_SCOPE)

add_library(gslerr STATIC EXCLUDE_FROM_ALL ${gslerr_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_errno.h gsl_message.h DESTINATION ${INSTALL_INC}/gsl)

