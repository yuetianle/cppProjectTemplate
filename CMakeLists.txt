# REFERENCE PROJECT CMAKELISTS.TXT
#
# @author  nvtienanh
project(UXA)
cmake_minimum_required(VERSION 2.8.12)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

enable_testing() # needed on top-level CMakeLists.txt

# Target doc definition
# The challenge here is that the sub projects must all define a custom target but with different names to avoid
# conflicts. We also want to be able to issue "make doc" from the top dir while being able to issue "make doc"
# in the subdirs *when* we compile only a subproject.
# We define as well a function AddDocTarget in cmake/DoxygenTarget.cmake
add_custom_target(doc) # DEPENDS docProjA docProjB) Note: with CMake 3.X the DEPENDS would work
ADD_DEPENDENCIES(doc docProjA docProjB docProjC)


INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/ProjA/include)
INCLUDE_DIRECTORIES(${CMAKE_BINARY_DIR}/ProjA/include)
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/ProjB/include)
INCLUDE_DIRECTORIES(${CMAKE_BINARY_DIR}/ProjB/include)
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/ProjC/include)
INCLUDE_DIRECTORIES(${CMAKE_BINARY_DIR}/ProjC/include)

add_subdirectory(ProjA) # Project A is independent
add_subdirectory(ProjB) # Project B is depend on Project A
add_subdirectory(ProjC) # Project C is independent
