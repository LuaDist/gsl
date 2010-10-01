
# Copy .h files into a gsl subdirectory so that #include <gsl/*.h> works.
FILE(GLOB_RECURSE HEADERLIST ${CMAKE_CURRENT_SOURCE_DIR}/../gsl*.h)
FOREACH(v ${HEADERLIST})
  GET_FILENAME_COMPONENT(dest ${v} NAME)
  CONFIGURE_FILE(${v} gsl/${dest} COPYONLY)
ENDFOREACH(v)


########### install files ###############



# clean: delete gsl*.h
