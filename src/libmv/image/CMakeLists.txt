# TODO(julien) remove this line, what's that for?
ADD_DEFINITIONS(-DTHIS_SOURCE_DIR="\\"${CMAKE_CURRENT_SOURCE_DIR}\\"")

IF(WIN32)
  INCLUDE_DIRECTORIES(
    ${JPEG_SOURCE_DIR}
    ${PNG_SOURCE_DIR}
    ${ZLIB_SOURCE_DIR}
  )
ENDIF(WIN32)

# define the source files
SET(IMAGE_SRC image.cc convolve.cc array_nd.cc)

# define the header files (make the headers appear in IDEs.)
FILE(GLOB IMAGE_HDRS *.h)

ADD_LIBRARY(image ${IMAGE_SRC} ${IMAGE_HDRS})


# make the name of debug libraries end in _d.
SET_TARGET_PROPERTIES(image PROPERTIES DEBUG_POSTFIX "_d")

# installation rules for the library
LIBMV_INSTALL_LIB(image)

MACRO (IMAGE_TEST NAME)
  LIBMV_TEST(${NAME} image)
ENDMACRO (IMAGE_TEST)

