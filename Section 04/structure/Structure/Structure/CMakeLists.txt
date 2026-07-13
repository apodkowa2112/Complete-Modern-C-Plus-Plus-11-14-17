add_executable(proj_Section_04_structure_Structure_Structure
  Source.cpp
)

target_include_directories(proj_Section_04_structure_Structure_Structure PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")
target_compile_features(proj_Section_04_structure_Structure_Structure PRIVATE cxx_std_17)
set_target_properties(proj_Section_04_structure_Structure_Structure PROPERTIES
  CXX_STANDARD 17
  CXX_STANDARD_REQUIRED YES
  CXX_EXTENSIONS NO
  OUTPUT_NAME "Structure"
)
