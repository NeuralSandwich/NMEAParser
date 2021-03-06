cmake_minimum_required (VERSION 3.0 FATAL_ERROR)

# Detect if clang is AppleClang or not
if(POLICY CMP0025)
  cmake_policy(SET CMP0025 NEW)
endif()

# Merge project and Version command
cmake_policy(SET CMP0048 NEW)
project (NMEAParser VERSION 1.0)

INCLUDE(CPack)

include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
else()
        message(STATUS "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")

#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wpedantic -Wshadow -Wpointer-arith -Wcast-qual -Wcast-align -Wsign-conversion -Wconversion")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Weverything -std=c++11 -Wno-c++98-compat -Wno-c++98-compat-pedantic -Wno-padded")

IF(BUILD_TESTING)
  add_definitions(-DDEBUG)
  add_subdirectory(gtest)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O0 -g3")
ENDIF(BUILD_TESTING)

add_subdirectory(lib)

IF (BUILD_TESTING)
  enable_testing()
  add_subdirectory(test)
ENDIF(BUILD_TESTING)
