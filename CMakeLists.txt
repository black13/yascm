cmake_minimum_required(VERSION 3.0)

project(yascm)

find_package(BISON REQUIRED)
find_package(FLEX REQUIRED)



add_custom_target(LEXER ALL 
    COMMAND flex -o ${CMAKE_CURRENT_BINARY_DIR}/yascm_flex.lex.c ${CMAKE_CURRENT_SOURCE_DIR}/yascm_flex.l
    )

add_custom_target(PARSER ALL
    COMMAND bison -o ${CMAKE_CURRENT_BINARY_DIR}/yascm_bison.tab.c -d ${CMAKE_CURRENT_SOURCE_DIR}/yascm_bison.y
    )

set(SOURCE_FILES ${SOURCE_FILES} ${CMAKE_CURRENT_BINARY_DIR}/yascm_flex.lex.c 
${CMAKE_CURRENT_BINARY_DIR}/yascm_bison.tab.c 
${CMAKE_CURRENT_SOURCE_DIR}/yascm.c
${CMAKE_CURRENT_SOURCE_DIR}/yascm.h)


add_executable(yasc ${SOURCE_FILES})
#bison -d yascm_bison.y -o yascm_bison.tab.c

target_include_directories(yasc
    PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)