cmake_minimum_required(VERSION 3.16)
project(log C)

set(CMAKE_C_STANDARD 11)

add_library(log STATIC log.c log.h)
set_target_properties(log PROPERTIES PUBLIC_HEADER "log.h")
INSTALL(TARGETS log
        LIBRARY DESTINATION "lib"
        PUBLIC_HEADER DESTINATION "include")