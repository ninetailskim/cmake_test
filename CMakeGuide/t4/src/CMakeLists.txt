INCLUDE_DIRECTORIES(/usr/include/hello)

ADD_EXECUTABLE(main main.c)

TARGET_LINK_LIBRARIES(main libhello.a)
# TARGET_LINK_LIBRARIES(main hello)
# TARGET_LINK_LIBRARIES(main libhello.so)