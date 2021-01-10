cmake_minimum_required(VERSION 2.8.12)
project(triangle)

add_library(Triangle SHARED triangle.c)
target_compile_definitions(Triangle PRIVATE -DTRILIBRARY -DANSI_DECLARATORS)
if(WIN32)
   target_compile_definitions(Triangle PRIVATE -DNO_TIMER)
endif()

# Generate position independent code
set_target_properties(Triangle PROPERTIES POSITION_INDEPENDENT_CODE ON)

set_target_properties(Triangle PROPERTIES PUBLIC_HEADER "triangle.h")
#set_target_properties(TetGen PROPERTIES PUBLIC_HEADER "tetgen.h")
install(TARGETS Triangle EXPORT TriangleTargets)
install(EXPORT TriangleTargets
 FILE Triangle.cmake
  NAMESPACE Triangle::
  DESTINATION lib/cmake/Triangle
 )

