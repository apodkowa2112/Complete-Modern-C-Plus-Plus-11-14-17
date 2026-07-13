add_executable(proj_Section_14_STL_Algorithms_Algorithms
  Source.cpp
)

target_include_directories(proj_Section_14_STL_Algorithms_Algorithms PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")
target_compile_features(proj_Section_14_STL_Algorithms_Algorithms PRIVATE cxx_std_17)
set_target_properties(proj_Section_14_STL_Algorithms_Algorithms PROPERTIES
  CXX_STANDARD 17
  CXX_STANDARD_REQUIRED YES
  CXX_EXTENSIONS NO
  OUTPUT_NAME "Algorithms"
)
