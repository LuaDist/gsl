# Copyright (C) 2007-2009 LuaDist.
# Submited by David Manura
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# For details see the COPYRIGHT file distributed with LuaDist.
# Please note that the package source code is licensed under its own license.
#
# Note: these CMakeLists.txt were originally generated with the
# assistance of am2cmake [1].
#
# [1] http://websvn.kde.org/trunk/KDE/kdesdk/cmake/scripts/am2cmake?revision=902353&view=markup

PROJECT (gsl C)
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
INCLUDE(dist.cmake)

# utility function:
# http://www.cmake.org/pipermail/cmake/2002-August/002948.html
macro(ASSERT test message)
  if(NOT ${test})
    message(FATAL_ERROR "FAILED ASSERT: ${message}")
  endif(NOT ${test})
endmacro(ASSERT)

if (MSVC)
  add_definitions(-D_CRT_SECURE_NO_WARNINGS -Dinline=__inline)
  # prevent math.h defining complex, causing problems in rowcol_source.c
  add_definitions(/Za)
  set(CMAKE_REQUIRED_DEFINITIONS ${CMAKE_REQUIRED_DEFINITIONS} /Za)
endif (MSVC)


# configure tests
INCLUDE(CheckSymbolExists)
INCLUDE(CheckIncludeFiles)
SET(BACKUP ${CMAKE_REQUIRED_DEFINITIONS})
SET(CMAKE_REQUIRED_DEFINITIONS ${CMAKE_REQUIRED_DEFINITIONS} -D_GNU_SOURCE=1)
  CHECK_SYMBOL_EXISTS(feenableexcept fenv.h HAVE_DECL_FEENABLEEXCEPT)
  CHECK_SYMBOL_EXISTS(fesettrapenable fenv.h HAVE_DECL_FESETTRAPENABLE)
SET(CMAKE_REQUIRED_DEFINITIONS ${BACKUP})
CHECK_SYMBOL_EXISTS(hypot math.h HAVE_DECL_HYPOT)
CHECK_SYMBOL_EXISTS(expm1 math.h HAVE_DECL_EXPM1)
CHECK_SYMBOL_EXISTS(acosh math.h HAVE_DECL_ACOSH)
CHECK_SYMBOL_EXISTS(asinh math.h HAVE_DECL_ASINH)
CHECK_SYMBOL_EXISTS(atanh math.h HAVE_DECL_ATANH)
CHECK_SYMBOL_EXISTS(ldexp math.h HAVE_DECL_LDEXP)
CHECK_SYMBOL_EXISTS(frexp math.h HAVE_DECL_FREXP)
CHECK_SYMBOL_EXISTS(isinf math.h HAVE_DECL_ISINF)
CHECK_SYMBOL_EXISTS(isfinite math.h HAVE_DECL_ISFINITE)
CHECK_INCLUDE_FILES(ieeefp.h HAVE_IEEEFP_H)
IF(${HAVE_FINITE_EXTRA})
  SET(FINITE_EXTRA ieeefp.h)
ENDIF(${HAVE_FINITE_EXTRA})
CHECK_SYMBOL_EXISTS(finite math.h ${FINITE_EXTRA} HAVE_DECL_FINITE)
CHECK_SYMBOL_EXISTS(isnan math.h HAVE_DECL_ISNAN)


configure_file(${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/config.h)

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/gsl_version.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/gsl_version.h)

#~2DO - variables not properly defined in file
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/gsl.pc.in ${CMAKE_CURRENT_BINARY_DIR}/gsl.pc)
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/gsl-config.in ${CMAKE_CURRENT_BINARY_DIR}/gsl-config
  COPYONLY #~2DO remove to allow variable substitution
)

SET (INSTALL_PKGCONFIG $(libdir)/pkgconfig)

include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_subdirectory(gsl)
add_subdirectory(utils)
add_subdirectory(sys)
add_subdirectory(test)
add_subdirectory(err)
add_subdirectory(const)
add_subdirectory(complex)
add_subdirectory(cheb)
add_subdirectory(block)
add_subdirectory(vector)
add_subdirectory(matrix)
add_subdirectory(permutation)
add_subdirectory(combination)
add_subdirectory(sort)
add_subdirectory(ieee-utils)
add_subdirectory(cblas)
add_subdirectory(blas)
add_subdirectory(linalg)
add_subdirectory(eigen)
add_subdirectory(specfunc)
add_subdirectory(dht)
add_subdirectory(qrng)
add_subdirectory(rng)
add_subdirectory(randist)
add_subdirectory(fft)
add_subdirectory(poly)
add_subdirectory(fit)
add_subdirectory(multifit)
add_subdirectory(statistics)
add_subdirectory(siman)
add_subdirectory(sum)
add_subdirectory(integration)
add_subdirectory(interpolation)
add_subdirectory(histogram)
add_subdirectory(ode-initval)
add_subdirectory(roots)
add_subdirectory(multiroots)
add_subdirectory(min)
add_subdirectory(multimin)
add_subdirectory(monte)
add_subdirectory(ntuple)
add_subdirectory(diff)
add_subdirectory(deriv)
add_subdirectory(cdf)
add_subdirectory(wavelet)
add_subdirectory(bspline)
add_subdirectory(doc)


########### next target ###############

SET(gsl_sublibs
  gslblock
  gslblas
  gslbspline
  gslcomplex
  gslcheb
  gsldht
  gsldiff
  gslderiv
  gsleigen
  gslerr
  gslfft
  gslfit
  gslhistogram
  gslieee-utils
  gslintegration
  gslinterpolation
  gsllinalg
  gslmatrix
  gslmin
  gslmonte
  gslmultifit
  gslmultimin
  gslmultiroots
  gslntuple
  gslode-initval
  gslpermutation
  gslcombination
  gslpoly
  gslqrng
  gslrandist
  gslrng
  gslroots
  gslsiman
  gslsort
  gslspecfunc
  gslstatistics
  gslsum
  gslsys
  gsltest
  utils
  gslvector
  gslcdf
  gslwavelet
)

set(gsl_LIB_SRCS version.c)
foreach(x ${gsl_sublibs})
  string(REPLACE gsl "" xx ${x})
  set(srcs ${${x}_STAT_SRCS})
  ASSERT(srcs ${x})
  foreach(fname ${${x}_STAT_SRCS})
    list(APPEND gsl_LIB_SRCS ${xx}/${fname})
  endforeach()
endforeach(x)
#foreach(x ${gsl_LIB_SRCS})
#  message(debug ${x})
#endforeach(x)

add_library(gsl SHARED ${gsl_LIB_SRCS} gsl.def)
set_target_properties(gsl PROPERTIES VERSION 1.0.0 SOVERSION 1)
IF(WIN32)
  target_link_libraries(gsl gslcblas)  #~ok?
ENDIF(WIN32)

install(TARGETS gsl ${INSTALL_TARGETS_DEFAULT_ARGS} DESTINATION ${INSTALL_LIB})


########### next target ###############

set(gsl-randist_SRCS gsl-randist.c)

add_executable(gsl-randist ${gsl-randist_SRCS})

target_link_libraries(gsl-randist gsl gslcblas)
IF(UNIX)
  target_link_libraries(gsl-randist m)  #~ok?
ENDIF(UNIX)

install(TARGETS gsl-randist ${INSTALL_TARGETS_DEFAULT_ARGS} DESTINATION ${INSTALL_BIN})


########### next target ###############

set(gsl-histogram_SRCS gsl-histogram.c)

add_executable(gsl-histogram ${gsl-histogram_SRCS})

target_link_libraries(gsl-histogram gsl gslcblas)
IF(UNIX)
  target_link_libraries(gsl-histogram m)  #~ok?
ENDIF(UNIX)

install(TARGETS gsl-histogram ${INSTALL_TARGETS_DEFAULT_ARGS} DESTINATION ${INSTALL_BIN})


########### install files ###############

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/gsl.pc DESTINATION ${INSTALL_DATA})
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/gsl-config DESTINATION ${INSTALL_DATA})
#install(FILES gsl.m4 DESTINATION /share/aclocal) #~ 2DO?
install(FILES test_gsl_histogram.sh DESTINATION ${INSTALL_DATA})
install(FILES gsl_math.h gsl_pow_int.h gsl_nan.h gsl_machine.h gsl_mode.h gsl_precision.h gsl_types.h gsl_version.h gsl_minmax.h gsl_inline.h DESTINATION ${INSTALL_INC}/gsl)
