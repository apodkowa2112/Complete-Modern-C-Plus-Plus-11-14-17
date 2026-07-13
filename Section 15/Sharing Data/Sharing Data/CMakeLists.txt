# Force CMake to use g++ for C++ builds
set(CMAKE_CXX_COMPILER "/usr/bin/g++" CACHE STRING "C++ compiler" FORCE)
add_executable(proj_Section_15_Sharing_Data_Sharing_Data
  Source.cpp
)

target_include_directories(proj_Section_15_Sharing_Data_Sharing_Data PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")
target_compile_features(proj_Section_15_Sharing_Data_Sharing_Data PRIVATE cxx_std_17)
set_target_properties(proj_Section_15_Sharing_Data_Sharing_Data PROPERTIES
  CXX_STANDARD 17
  CXX_STANDARD_REQUIRED YES
  CXX_EXTENSIONS NO
  OUTPUT_NAME "Sharing_Data"
)
