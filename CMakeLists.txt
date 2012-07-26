# Copyright (C) 2007-2012 LuaDist.
# Created by David Manura, Peter Drahoš
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# For details see the COPYRIGHT file distributed with LuaDist.
# Please note that the package source code is licensed under its own license.
#
# Note: these CMakeLists.txt were originally generated with the
# assistance of am2cmake [1].
#
# [1] http://websvn.kde.org/trunk/KDE/kdesdk/cmake/scripts/am2cmake?revision=902353&view=markup

project ( gsl C )
cmake_minimum_required ( VERSION 2.8 )
include ( cmake/dist.cmake )

# utility function:
# http://www.cmake.org/pipermail/cmake/2002-August/002948.html
macro ( ASSERT test message )
if ( NOT ${test} )
  message ( FATAL_ERROR "FAILED ASSERT: ${message}" )
endif ( NOT ${test} )
endmacro ( ASSERT )

if ( MSVC )
  add_definitions ( -D_CRT_SECURE_NO_WARNINGS -Dinline=__inline )
  # prevent math.h defining complex, causing problems in rowcol_source.c
  add_definitions ( /Za )
  set ( CMAKE_REQUIRED_DEFINITIONS ${CMAKE_REQUIRED_DEFINITIONS} /Za )
endif ( MSVC )

# configure tests
include ( CheckSymbolExists )
include ( CheckIncludeFiles )
set ( BACKUP ${CMAKE_REQUIRED_DEFINITIONS} )
set ( CMAKE_REQUIRED_DEFINITIONS ${CMAKE_REQUIRED_DEFINITIONS} -D_GNU_SOURCE=1 )
check_symbol_exists ( feenableexcept fenv.h HAVE_DECL_FEENABLEEXCEPT )
check_symbol_exists ( fesettrapenable fenv.h HAVE_DECL_FESETTRAPENABLE )
set ( CMAKE_REQUIRED_DEFINITIONS ${BACKUP} )
check_symbol_exists ( hypot math.h HAVE_DECL_HYPOT )
check_symbol_exists ( expm1 math.h HAVE_DECL_EXPM1 )
check_symbol_exists ( acosh math.h HAVE_DECL_ACOSH )
check_symbol_exists ( asinh math.h HAVE_DECL_ASINH )
check_symbol_exists ( atanh math.h HAVE_DECL_ATANH )
check_symbol_exists ( ldexp math.h HAVE_DECL_LDEXP )
check_symbol_exists ( frexp math.h HAVE_DECL_FREXP )
check_symbol_exists ( isinf math.h HAVE_DECL_ISINF )
check_symbol_exists ( isfinite math.h HAVE_DECL_ISFINITE )
check_include_files ( ieeefp.h HAVE_IEEEFP_H )
if ( ${HAVE_FINITE_EXTRA} )
  set ( FINITE_EXTRA ieeefp.h )
endif ( ${HAVE_FINITE_EXTRA} )
check_symbol_exists ( finite math.h ${FINITE_EXTRA} HAVE_DECL_FINITE )
check_symbol_exists ( isnan math.h HAVE_DECL_ISNAN )

configure_file ( ${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/config.h )

configure_file ( ${CMAKE_CURRENT_SOURCE_DIR}/gsl_version.h.cmake ${CMAKE_CURRENT_BINARY_DIR}/gsl_version.h )

#~2DO - variables not properly defined in file
configure_file ( ${CMAKE_CURRENT_SOURCE_DIR}/gsl.pc.in ${CMAKE_CURRENT_BINARY_DIR}/gsl.pc )
configure_file ( ${CMAKE_CURRENT_SOURCE_DIR}/gsl-config.in ${CMAKE_CURRENT_BINARY_DIR}/gsl-config 
  COPYONLY #~2DO remove to allow variable substitution
)

set ( INSTALL_PKGCONFIG $ ( libdir ) /pkgconfig )

include_directories ( ${CMAKE_CURRENT_BINARY_DIR} )
include_directories ( ${CMAKE_CURRENT_SOURCE_DIR} )

add_subdirectory ( gsl )
add_subdirectory ( utils )
add_subdirectory ( sys )
add_subdirectory ( test )
add_subdirectory ( err )
add_subdirectory ( const )
add_subdirectory ( complex )
add_subdirectory ( cheb )
add_subdirectory ( block )
add_subdirectory ( vector )
add_subdirectory ( matrix )
add_subdirectory ( permutation )
add_subdirectory ( combination )
add_subdirectory ( sort )
add_subdirectory ( ieee-utils )
add_subdirectory ( cblas )
add_subdirectory ( blas )
add_subdirectory ( linalg )
add_subdirectory ( eigen )
add_subdirectory ( specfunc )
add_subdirectory ( dht )
add_subdirectory ( qrng )
add_subdirectory ( rng )
add_subdirectory ( randist )
add_subdirectory ( fft )
add_subdirectory ( poly )
add_subdirectory ( fit )
add_subdirectory ( multifit )
add_subdirectory ( statistics )
add_subdirectory ( siman )
add_subdirectory ( sum )
add_subdirectory ( integration )
add_subdirectory ( interpolation )
add_subdirectory ( histogram )
add_subdirectory ( ode-initval )
add_subdirectory ( roots )
add_subdirectory ( multiroots )
add_subdirectory ( min )
add_subdirectory ( multimin )
add_subdirectory ( monte )
add_subdirectory ( ntuple )
add_subdirectory ( diff )
add_subdirectory ( deriv )
add_subdirectory ( cdf )
add_subdirectory ( wavelet )
add_subdirectory ( bspline )
add_subdirectory ( doc )

########### next target ###############

set ( gsl_sublibs gslblock gslblas gslbspline gslcomplex gslcheb gsldht gsldiff gslderiv 
  gsleigen gslerr gslfft gslfit gslhistogram gslieee-utils gslintegration gslinterpolation 
  gsllinalg gslmatrix gslmin gslmonte gslmultifit gslmultimin gslmultiroots gslntuple 
  gslode-initval gslpermutation gslcombination gslpoly gslqrng gslrandist gslrng 
  gslroots gslsiman gslsort gslspecfunc gslstatistics gslsum gslsys gsltest utils 
  gslvector gslcdf gslwavelet )

set ( gsl_LIB_SRCS version.c )
foreach ( x ${gsl_sublibs} )
string ( REPLACE gsl "" xx ${x} )
set ( srcs ${${x}_STAT_SRCS} )
assert ( srcs ${x} )
foreach ( fname ${${x}_STAT_SRCS} )
list ( APPEND gsl_LIB_SRCS ${xx}/${fname} )
endforeach ( )
endforeach ( x )
#foreach(x ${gsl_LIB_SRCS})
#  message(debug ${x})
#endforeach(x)

add_library ( gsl ${gsl_LIB_SRCS} gsl.def )
set_target_properties ( gsl PROPERTIES VERSION 1.0.0 SOVERSION 1 )
if ( WIN32 )
  target_link_libraries ( gsl gslcblas )
  #~ok?
endif ( WIN32 )

install_library ( gsl )

########### next target ###############

set ( gsl-randist_SRCS gsl-randist.c )

add_executable ( gsl-randist ${gsl-randist_SRCS} )

target_link_libraries ( gsl-randist gsl gslcblas )
if ( UNIX )
  target_link_libraries ( gsl-randist m )
  #~ok?
endif ( UNIX )

install_executable ( gsl-randist )

########### next target ###############

set ( gsl-histogram_SRCS gsl-histogram.c )

add_executable ( gsl-histogram ${gsl-histogram_SRCS} )

target_link_libraries ( gsl-histogram gsl gslcblas )
if ( UNIX )
  target_link_libraries ( gsl-histogram m )
  #~ok?
endif ( UNIX )

install_executable ( gsl-histogram )

########### install files ###############

install_foo ( ${CMAKE_CURRENT_BINARY_DIR}/gsl.pc ${CMAKE_CURRENT_BINARY_DIR}/gsl-config )
install_test ( test_gsl_histogram.sh )
install_header ( gsl_math.h gsl_pow_int.h gsl_nan.h gsl_machine.h gsl_mode.h gsl_precision.h 
  gsl_types.h gsl_version.h gsl_minmax.h gsl_inline.h INTO gsl )
