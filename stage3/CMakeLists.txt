add_library(stage3 STATIC array_range_check.cc
                        constant_folding.cc
                        declaration_check.cc
                        fill_candidate_datatypes.cc
                        forced_narrow_candidate_datatypes.cc
                        narrow_candidate_datatypes.cc
                        remove_forward_dependencies.cc
                        case_elements_check.cc
                        datatype_functions.cc
                        enum_declaration_check.cc
                        flow_control_analysis.cc
                        lvalue_check.cc
                        print_datatypes_error.cc
                        stage3.cc
)

target_include_directories(stage3 PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
