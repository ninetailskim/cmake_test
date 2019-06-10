cmake_minimum_required (VERSION 2.8)
project(Demo)


configure_file(	
	"${PROJECT_SOURCE_DIR}/config.h.in"
	"${PROJECT_BINARY_DIR}/config.h"
)

option (USE_MYMATH
	"Use provided math implementation" ON)

if (USE_MYMATH)
	include_directories ("${PROJECT_SOURCE_DIR}/math")
	add_subdirectory (math)
	set (EXTRA_LIBS ${EXTRA_LIBS} MathFunctions)
endif (USE_MATH)

aux_source_directory(. DIR_SRCS)

add_executable(demo ${DIR_SRCS})

target_link_libraries(demo MathFunctions)
