# Force CMake to use g++ for C++ builds
set(CMAKE_CXX_COMPILER "/usr/bin/g++" CACHE STRING "C++ compiler" FORCE)
add_executable(proj_Section_02_Pointers_Pointers_Pointers
  Source.cpp
)

target_include_directories(proj_Section_02_Pointers_Pointers_Pointers PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")
target_compile_features(proj_Section_02_Pointers_Pointers_Pointers PRIVATE cxx_std_17)
set_target_properties(proj_Section_02_Pointers_Pointers_Pointers PROPERTIES
  CXX_STANDARD 17
  CXX_STANDARD_REQUIRED YES
  CXX_EXTENSIONS NO
  OUTPUT_NAME "Pointers"
)
