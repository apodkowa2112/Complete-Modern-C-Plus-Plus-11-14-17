      cmake_minimum_required(VERSION 3.16)
      project(ModernCppTutorials LANGUAGES CXX)

      set(CMAKE_CXX_STANDARD 17)
      set(CMAKE_CXX_STANDARD_REQUIRED ON)
      set(CMAKE_CXX_EXTENSIONS OFF)
      set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

      set(_generated_subdirs
        "Section 02/BasicIO/BasicIO"
        "Section 02/Default Function Args/DefaultFunctionArgs/DefaultFunctionArgs"
        "Section 02/First Program/First Program"
        "Section 02/Function Overloading/Function Overloading/Function Overloading"
        "Section 02/Function Pointers/Function Pointer/Function Pointer"
        "Section 02/Inline functions/Inline Functions/Inline Functions"
        "Section 02/Namespace/Namespace/Namespace"
        "Section 02/Pointers/Pointers/Pointers"
        "Section 02/Range-based for/ForEach/ForEach"
        "Section 02/Ref Vs Ptr/SwapFunction/SwapFunction"
        "Section 02/Reference/Reference/Reference"
        "Section 02/auto/AutoKeyword/AutoKeyword"
        "Section 02/const Qualifier and Compound Types/const qualifer/const qualifer"
        "Section 03/MemMgmtC/MemMgmtC"
        "Section 04/Copy Ctor/Copy Ctor"
        "Section 04/Default and Deleted Functions/New Class Keywords/New Class Keywords"
        "Section 04/Lvalues and rvalues/RValues/RValues"
        "Section 04/Move Semantics Impl/Copy Ctor - Complete/Copy Ctor"
        "Section 04/RuleofFive/RuleofFive"
        "Section 04/Static/Car Abstraction/Car Abstraction"
        "Section 04/class/Car/Car"
        "Section 04/structure/Structure/Structure"
        "Section 05/Lvalues and rvalues/RValues/RValues"
        "Section 05/Move Semantics Impl/Copy Ctor - Complete/Copy Ctor"
        "Section 05/RuleofFive/RuleofFive"
        "Section 06/Operator Overloading/Copy Ctor"
        "Section 06/UserDefConversions/UserDefConversions"
        "Section 07/CircularRef/CircularRef"
        "Section 07/More Features/More Features"
        "Section 07/shared_ptr/shared_ptr"
        "Section 07/unique_ptr/unique_ptr"
        "Section 07/weak_ptr/weak_ptr"
        "Section 08/StringStreams/StringStreams"
        "Section 08/Strings/Strings"
        "Section 08/UserDefinedLiterals/UserDefinedLiterals"
        "Section 08/Vector/Vector"
        "Section 08/constexpr/constexpr/constexpr"
        "Section 08/enums/enums"
        "Section 08/initializer_list/InitializerList/InitializerList"
        "Section 09/Account/Account"
        "Section 10/ExceptionHandling-noexcept/ExceptionHandling-noexcept"
        "Section 10/Exceptions in ctors/ExceptionHandlingII/ExceptionHandlingII"
        "Section 10/Nested Exceptions/Exception Handling/Exception Handling"
        "Section 11/Binary Files/FileIO-BinaryFiles/FileIO-BinaryFiles"
        "Section 11/Error Handling/File IO/File IO"
        "Section 12/Aliases/Aliases/Aliases"
        "Section 12/Basics/Basics"
        "Section 12/Class Exp Spec - II/Class Template ExSpecialization/Class Template ExSpecialization"
        "Section 12/Class Templates/Class Templates/Class Templates"
        "Section 12/Partial Spec/Class Template ParSpecializatoin/Class Template ParSpecializatoin"
        "Section 12/Perfect Forwarding - II/Perfect forwarding/Perfect forwarding"
        "Section 12/Variadic Templates - II/Variadic Templates/Variadic Templates"
        "Section 13/Capture List/CaptureList/CaptureList"
        "Section 13/Function Objects/Function Objects/Function Objects"
        "Section 13/Lambda Basics/Lambda Basics/Lambda Basics"
        "Section 14/STL/Algorithms/Algorithms"
        "Section 14/STL/AssociativeContainers/AssociativeContainers"
        "Section 14/STL/ContainerChanges/ContainerChanges"
        "Section 14/STL/SequenceContainers/SequenceContainers"
        "Section 14/STL/UnorderedContainers/UnorderedContainers"
        "Section 15/Async/Async"
        "Section 15/PromiseFuture/PromiseFuture"
        "Section 15/Sharing Data/Sharing Data"
        "Section 15/ThreadClass/ThreadClass"
        "Section 15/Threads/Threads"
      )

      foreach(_dir IN LISTS _generated_subdirs)
        if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/${_dir}/CMakeLists.txt")
          add_subdirectory("${_dir}")
        endif()
      endforeach()
