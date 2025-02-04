add_library(stage4_c STATIC generate_c.cc
                         ${COMMON_STAGE4_SRC}
)

#target_include_directories(stage3 PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
