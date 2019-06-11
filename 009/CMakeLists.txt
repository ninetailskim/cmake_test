cmake_minimum_required(VERSION 2.8)

project(Demo1)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

include (${CMAKE_ROOT}/Modules/CheckFunctionExists.cmake)
check_function_exists (pow HAVE_POW)
#here , i don't understand

configure_file(
    "${PROJECT_SOURCE_DIR}/config.h.in"
    "${PROJECT_BINARY_DIR}/config.h"
)

message(${CMAKE_ROOT})
message(${PROJECT_SOURCE_DIR})
message(${PROJECT_BINARY_DIR})
message(${PROJECT_NAME})
message(${CMAKE_CURRENT_SOURCE_DIR})
message(${CMAKE_CURRENT_BINARY_DIR})
message(${CMAKE_CURRENT_LIST_DIR})
message(${CMAKE_CURRENT_LIST_LINE})

option (USE_MYMATH "Use provided math implementation" ON)

if (USE_MYMATH)
    include_directories ("${PROJECT_SOURCE_DIR}/math")
    add_subdirectory(math)
    set (EXTRA_LIBS ${EXTRA_LIBS} MathFunctions)
endif (USE_MYMATH)

# add_executable(Demo main.cc MathFunctions.cc)
aux_source_directory(. DIR_SRCS)

add_executable(Demo ${DIR_SRCS})

target_link_libraries(Demo ${EXTRA_LIBS})

install (TARGETS Demo DESTINATION bin)
install (FILES "${PROJECT_BINARY_DIR}/config.h" DESTINATION include)

enable_testing()

#add_test (test_run Demo 5 2)

#add_test (test_usage Demo)
#set_tests_properties (test_usage PROPERTIES PASS_REGULAR_EXPRESSION "Usage: .* base exponent")

#add_test (test_5_2 Demo 5 2)
#set_tests_properties (test_5_2 PROPERTIES PASS_REGULAR_EXPRESSION "is 25")

#add_test (test_10_5 Demo 10 5)
#set_tests_properties (test_10_5 PROPERTIES PASS_REGULAR_EXPRESSION "is 100000")

#add_test(test_2_10 Demo 2 10)
#set_tests_properties (test_2_10 PROPERTIES PASS_REGULAR_EXPRESSION "is 1024")

#其中 PASS_REGULAR_EXPRESSION 用来测试输出是否包含后面跟着的字符串。

macro (do_test arg1 arg2 result)
    add_test(test_${arg1}_${arg2} Demo ${arg1} ${arg2})
    set_tests_properties (test_${arg1}_${arg2} PROPERTIES PASS_REGULAR_EXPRESSION ${result})
endmacro (do_test)

do_test (5 2 "is 25")
do_test (10 5 "is 10000")
do_test (2 10 "is 1024")