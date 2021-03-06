# CMakeLists.txt --- CMake project settings
#    ex) cmake -G "Visual Studio 9 2008" .
#    ex) cmake -DCMAKE_BUILD_TYPE=Release -G "MSYS Makefiles" .
##############################################################################

# CMake minimum version
cmake_minimum_required(VERSION 2.4)

# enable CTest
enable_testing()

# use new policy
cmake_policy(SET CMP0054 NEW)

# project name and language
project(EbnfParser CXX)

# check build type
if (NOT CMAKE_BUILD_TYPE)
    message(STATUS "No build type selected, default to Debug")
    set(CMAKE_BUILD_TYPE "Debug")
endif()

# make uppercase string of build type
string(TOUPPER "${CMAKE_BUILD_TYPE}" uppercase_CMAKE_BUILD_TYPE)

# check build type again
if (NOT uppercase_CMAKE_BUILD_TYPE MATCHES "^(DEBUG|RELEASE|RELWITHDEBINFO|MINSIZEREL)$")
    message(FATAL_ERROR "Invalid value for CMAKE_BUILD_TYPE: ${CMAKE_BUILD_TYPE}")
endif()

# define NDEBUG
string(CONCAT CMAKE_C_FLAGS_RELEASE " -DNDEBUG")
string(CONCAT CMAKE_C_FLAGS_RELWITHDEBINFO " -DNDEBUG")
string(CONCAT CMAKE_C_FLAGS_MINSIZEREL " -DNDEBUG")
string(CONCAT CMAKE_CXX_FLAGS_RELEASE " -DNDEBUG")
string(CONCAT CMAKE_CXX_FLAGS_RELWITHDEBINFO " -DNDEBUG")
string(CONCAT CMAKE_CXX_FLAGS_MINSIZEREL " -DNDEBUG")

# set output directory (build/)
set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})

##############################################################################

add_executable(EbnfParser EbnfParser.cpp)
add_executable(EbnfParseTest EbnfParseTest.cpp)
add_executable(EbnfCompareTest EbnfCompareTest.cpp)
add_executable(EbnfJoinTest EbnfJoinTest.cpp)

add_test(NAME EbnfParseTest COMMAND EbnfParseTest)
add_test(NAME EbnfCompareTest COMMAND EbnfCompareTest)
add_test(NAME EbnfJoinTest COMMAND EbnfJoinTest)

##############################################################################
