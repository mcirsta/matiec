find_package(FLEX REQUIRED)
find_package(BISON REQUIRED)

set(LEXER_INPUT ${CMAKE_CURRENT_SOURCE_DIR}/iec_flex.ll)
set(LEXER_OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/iec_flex.cc)
set(FLEX_EXECUTABLE flex)

# Add a custom command to run Flex
add_custom_command(
    OUTPUT ${LEXER_OUTPUT}
    COMMAND ${FLEX_EXECUTABLE} -o ${LEXER_OUTPUT} ${LEXER_INPUT}
    DEPENDS ${LEXER_INPUT}
    COMMENT "Generating iec_flex.cc from iec_flex.ll"
)

set(PARSER_INPUT ${CMAKE_CURRENT_SOURCE_DIR}/iec_bison.yy)
set(PARSER_OUTPUT_SOURCE ${CMAKE_CURRENT_BINARY_DIR}/iec_bison.cc)
set(PARSER_OUTPUT_HEADER ${CMAKE_CURRENT_BINARY_DIR}/iec_bison.hh)  # Bison-generated header

# Add a custom command to run Bison
add_custom_command(
    OUTPUT ${PARSER_OUTPUT_SOURCE} ${PARSER_OUTPUT_HEADER}
    COMMAND ${BISON_EXECUTABLE} -o ${PARSER_OUTPUT_SOURCE} --defines=${PARSER_OUTPUT_HEADER} ${PARSER_INPUT}
    DEPENDS ${PARSER_INPUT}
    COMMENT "Generating iec_bison.cc and parser.hpp from iec_bison.yy"
)


# Add the generated files to the list of sources
set(STAGE12_SOURCES
    ${LEXER_OUTPUT}
    ${PARSER_OUTPUT_SOURCE}
    create_enumtype_conversion_functions.cc
    stage1_2.cc
)

add_library(stage1_2 STATIC ${STAGE12_SOURCES})
target_include_directories(stage1_2 PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(stage1_2 PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_compile_definitions(stage1_2 PRIVATE DEFAULT_LIBDIR="lib")
