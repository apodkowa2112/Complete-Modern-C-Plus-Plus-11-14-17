add_executable(proj_Section_08_Strings_Strings
  Source.cpp
)

target_include_directories(proj_Section_08_Strings_Strings PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")
target_compile_features(proj_Section_08_Strings_Strings PRIVATE cxx_std_17)
set_target_properties(proj_Section_08_Strings_Strings PROPERTIES
  CXX_STANDARD 17
  CXX_STANDARD_REQUIRED YES
  CXX_EXTENSIONS NO
  OUTPUT_NAME "Strings"
)
