cmake_minimum_required(VERSION 3.5)
project(NearTree LANGUAGES C CXX)

# Global definitions
add_definitions(-DCNEARTREE_SAFE_TRIANG=1)

# Include current directory for headers
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

# Find CVector (required for the C implementation)
find_path(CVECTOR_INCLUDE_DIR CVector.h)
find_library(CVECTOR_LIBRARY CVector)

if(CVECTOR_INCLUDE_DIR AND CVECTOR_LIBRARY)
    message(STATUS "Found CVector: ${CVECTOR_INCLUDE_DIR}, ${CVECTOR_LIBRARY}")
    include_directories(${CVECTOR_INCLUDE_DIR})

    # CNearTree Library
    add_library(CNearTree CNearTree.c)
    target_link_libraries(CNearTree ${CVECTOR_LIBRARY} m)

    # C Examples/Tests
    add_executable(CMain main.c)
    target_link_libraries(CMain CNearTree)

    add_executable(CNearTreeTest CNearTreeTest.c)
    target_link_libraries(CNearTreeTest CNearTree)

    add_executable(CNearTreeTestInst CNearTreeTest.c)
    target_compile_definitions(CNearTreeTestInst PRIVATE CNEARTREE_INSTRUMENTED)
    target_link_libraries(CNearTreeTestInst CNearTree)

    install(TARGETS CNearTree
            DESTINATION lib)
else()
    message(WARNING "CVector not found. C-based targets (CNearTree library, CMain, CNearTreeTest) will not be built.")
endif()

# C++ Examples/Tests
# v.cpp is a helper used by all C++ examples
set(CPP_COMMON_SRC v.cpp)

add_executable(CPPMain main.cpp ${CPP_COMMON_SRC})
target_link_libraries(CPPMain m)

add_executable(CPPMain_Flip main_flip.cpp ${CPP_COMMON_SRC})
target_link_libraries(CPPMain_Flip m)

# CPPNearTreeTest variants
macro(add_cpp_test_variant name)
    add_executable(${name} CNearTreeTest.cpp ${CPP_COMMON_SRC})
    target_link_libraries(${name} m)
    if(ARGN)
        target_compile_definitions(${name} PRIVATE ${ARGN})
    endif()
endmacro()

add_cpp_test_variant(CPPNearTreeTest)
add_cpp_test_variant(CPPNearTreeTest_2SAMP CNEARTREE_DIMSAMPLES=2)
add_cpp_test_variant(CPPNearTreeTest_6SAMP CNEARTREE_DIMSAMPLES=6)
add_cpp_test_variant(CPPNearTreeTest_8SAMP CNEARTREE_DIMSAMPLES=8)
add_cpp_test_variant(CPPNearTreeTestInst CNEARTREE_INSTRUMENTED)
add_cpp_test_variant(CPPNearTreeTestInstFlip CNEARTREE_INSTRUMENTED CNEARTREE_FORCEFLIP)
add_cpp_test_variant(CPPNearTreeTestInstNoDefer CNEARTREE_INSTRUMENTED CNEARTREE_NODEFER)
add_cpp_test_variant(CPPNearTreeTestInstNoFlip CNEARTREE_INSTRUMENTED CNEARTREE_NOFLIP)
add_cpp_test_variant(CPPNearTreeTestInstNoFlipNoDefer CNEARTREE_INSTRUMENTED CNEARTREE_NOFLIP CNEARTREE_NODEFER)

# Installation
install(FILES TNear.h CNearTree.h rhrand.h triple.h v.h
        DESTINATION include)
