
########### next target ###############

set(utils_STAT_SRCS system.h placeholder.c)

add_library(utils STATIC EXCLUDE_FROM_ALL ${utils_STAT_SRCS})
set(utils_STAT_SRCS ${utils_STAT_SRCS} PARENT_SCOPE)

########### install files ###############

