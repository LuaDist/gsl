
########### next target ###############

set(gslrandist_STAT_SRCS
    bernoulli.c
    beta.c
    bigauss.c
    binomial.c
    cauchy.c
    chisq.c
    dirichlet.c
    discrete.c
    erlang.c
    exponential.c
    exppow.c
    fdist.c
    flat.c
    gamma.c
    gauss.c
    gausszig.c
    gausstail.c
    geometric.c
    gumbel.c
    hyperg.c
    laplace.c
    levy.c
    logarithmic.c
    logistic.c
    lognormal.c
    multinomial.c
    nbinomial.c
    pareto.c
    pascal.c
    poisson.c
    rayleigh.c
    shuffle.c
    sphere.c
    tdist.c
    weibull.c
    landau.c
    binomial_tpe.c)
set(gslrandist_STAT_SRCS ${gslrandist_STAT_SRCS} PARENT_SCOPE)

add_library(gslrandist STATIC EXCLUDE_FROM_ALL ${gslrandist_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslrandist gslrng gslspecfunc gslintegration gslcomplex gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_randist.h DESTINATION ${INSTALL_INC}/gsl)

