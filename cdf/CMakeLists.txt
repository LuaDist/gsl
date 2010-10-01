

########### next target ###############

set(gslcdf_STAT_SRCS
    beta.c
    betainv.c
    cauchy.c
    cauchyinv.c
    chisq.c
    chisqinv.c
    exponential.c
    exponentialinv.c
    exppow.c
    fdist.c
    fdistinv.c
    flat.c
    flatinv.c
    gamma.c
    gammainv.c
    gauss.c
    gaussinv.c
    gumbel1.c
    gumbel1inv.c
    gumbel2.c
    gumbel2inv.c
    laplace.c
    laplaceinv.c
    logistic.c
    logisticinv.c
    lognormal.c
    lognormalinv.c
    pareto.c
    paretoinv.c
    rayleigh.c
    rayleighinv.c
    tdist.c
    tdistinv.c
    weibull.c
    weibullinv.c
    binomial.c
    poisson.c
    geometric.c
    nbinomial.c
    pascal.c
    hypergeometric.c)
set(gslcdf_STAT_SRCS ${gslcdf_STAT_SRCS} PARENT_SCOPE)

add_library(gslcdf STATIC EXCLUDE_FROM_ALL ${gslcdf_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslcdf gslrandist gslrng gslspecfunc gslcomplex gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_cdf.h  DESTINATION ${INSTALL_INC}/gsl)

