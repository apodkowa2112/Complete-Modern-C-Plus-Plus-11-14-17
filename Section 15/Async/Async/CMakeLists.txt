      add_executable(proj_Section_15_Async_Async
        Source.cpp
main.cpp
      )

      target_include_directories(proj_Section_15_Async_Async PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")
      target_compile_features(proj_Section_15_Async_Async PRIVATE cxx_std_17)
      set_target_properties(proj_Section_15_Async_Async PROPERTIES
        CXX_STANDARD 17
        CXX_STANDARD_REQUIRED YES
        CXX_EXTENSIONS NO
        OUTPUT_NAME "Async"
      )
