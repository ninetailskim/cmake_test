cmake_minimum_required (VERSION 2.8)

project (server)

aux_source_directory(. DIS_SRCS)

set(INC_DIR /usr/local/include/)
set(LINK_DIR /usr/local/lib)

include_directories(${INC_DIR})
link_directories(${LINK_DIR})
link_libraries(ev)

add_executable(server ${DIR_SRCS})

target_link_libraries(server ev)
