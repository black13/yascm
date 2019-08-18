cmake_minimum_required(VERSION 3.0)

project(yascm)

find_package(BISON REQUIRED)
find_package(FLEX REQUIRED)

BISON_TARGET(MyParser yascm_bison.y ${CMAKE_CURRENT_BINARY_DIR}/yascm_bison.tab.c COMPILE_FLAGS -d)
FLEX_TARGET(MyScanner yascm_flex.l  ${CMAKE_CURRENT_BINARY_DIR}/yascm_flex.lex.c )
ADD_FLEX_BISON_DEPENDENCY(MyScanner MyParser)

 include_directories(${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR})
 add_executable(yascm
    yascm.c
    yascm.h
    ${BISON_MyParser_OUTPUTS}
    ${FLEX_MyScanner_OUTPUTS}
 )

