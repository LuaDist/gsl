

########### next target ###############

set(gslhistogram_STAT_SRCS
    add.c
    get.c
    init.c
    params.c
    reset.c
    file.c
    pdf.c
    gsl_histogram.h
    add2d.c
    get2d.c
    init2d.c
    params2d.c
    reset2d.c
    file2d.c
    pdf2d.c
    gsl_histogram2d.h
    calloc_range.c
    calloc_range2d.c
    copy.c
    copy2d.c
    maxval.c
    maxval2d.c
    oper.c
    oper2d.c
    stat.c
    stat2d.c)
set(gslhistogram_STAT_SRCS ${gslhistogram_STAT_SRCS} PARENT_SCOPE)

add_library(gslhistogram STATIC EXCLUDE_FROM_ALL ${gslhistogram_STAT_SRCS})


########### next target ###############

set(test_SRCS
    test.c
    test1d.c
    test2d.c
    test1d_resample.c
    test2d_resample.c
    test1d_trap.c
    test2d_trap.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslhistogram gslblock gslieeeutils gslerr gsltest gslsys)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_histogram.h gsl_histogram2d.h DESTINATION ${INSTALL_INC}/gsl)

