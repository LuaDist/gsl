

########### next target ###############

set(gslblock_STAT_SRCS init.c file.c block.c)
set(gslblock_STAT_SRCS ${gslblock_STAT_SRCS} PARENT_SCOPE)

add_library(gslblock STATIC EXCLUDE_FROM_ALL ${gslblock_STAT_SRCS})


########### next target ###############

set(test_SRCS test.c)

if(KDE4_BUILD_TESTS)

add_executable(test ${test_SRCS})

target_link_libraries(test gslblock gslieeeutils gslerr gsltest gslsys utils)

endif(KDE4_BUILD_TESTS)

########### install files ###############

install(FILES  gsl_block.h gsl_block_char.h gsl_block_complex_double.h gsl_block_complex_float.h gsl_block_complex_long_double.h gsl_block_double.h gsl_block_float.h gsl_block_int.h gsl_block_long.h gsl_block_long_double.h gsl_block_short.h gsl_block_uchar.h gsl_block_uint.h gsl_block_ulong.h gsl_block_ushort.h gsl_check_range.h DESTINATION ${INSTALL_INC}/gsl)

