add_library(stage4_iec STATIC generate_iec.cc
                         ${COMMON_STAGE4_SRC}
)

#target_include_directories(stage3 PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
