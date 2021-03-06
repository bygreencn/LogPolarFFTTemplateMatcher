# ----------------------------------------------------------------------------
# ����������� ������ CMake, ��������� ���������� ���� ����
# ----------------------------------------------------------------------------
cmake_minimum_required(VERSION 2.8)

set (PROJ_NAME LogPolarFFTTemplateMatching)

project(${PROJ_NAME})
set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})
# ---------------------------------------------------------------------------- 
# ������������, ��� FindOpenCV.cmake ���������� �� ������ CMAKE_MODULE_PATH.
# ----------------------------------------------------------------------------
  FIND_PACKAGE(OpenCV)
# ----------------------------------------------------------------------------  
# ���� ��� .cpp � .h ����� � ��������� �� � ��� ������ 
# ----------------------------------------------------------------------------
  set(folder_source fftm.cpp test.cpp example.cpp)
  set(folder_header fftm.hpp)
  SOURCE_GROUP("Source Files" FILES ${folder_source})
  SOURCE_GROUP("Header Files" FILES ${folder_header})
# ----------------------------------------------------------------------------  
# ������� ������
# ----------------------------------------------------------------------------
  ADD_EXECUTABLE(${PROJ_NAME}_example fftm.cpp example.cpp fftm.hpp)
# ----------------------------------------------------------------------------
# ��������� Lib-� opencv 
# ---------------------------------------------------------------------------- 
  TARGET_LINK_LIBRARIES(${PROJ_NAME}_example ${OpenCV_LIBS})

OPTION(BUILD_TEST "Build test" OFF) 

if(BUILD_TEST)
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})
# ----------------------------------------------------------------------------  
# ������� ������
# ----------------------------------------------------------------------------
  ADD_EXECUTABLE(${PROJ_NAME}_test fftm.cpp test.cpp fftm.hpp)
# ----------------------------------------------------------------------------
# ��������� Lib-� opencv 
# ---------------------------------------------------------------------------- 
  TARGET_LINK_LIBRARIES(${PROJ_NAME}_test ${OpenCV_LIBS} ${GTEST_BOTH_LIBRARIES})
endif()