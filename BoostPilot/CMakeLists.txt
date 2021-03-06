cmake_minimum_required(VERSION 3.5)

set(PROJECT_VERSION "0.0.1")
project(BoostPilot
        VERSION ${PROJECT_VERSION}
        LANGUAGES CXX)

if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GUN" OR
    "${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
    set(warnings "-Wall -Wextra -Werror")
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
    set(warnings "/W4 /WX /EHsc")
endif()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
set(CMAKE_CXX_STANDARD 11)
# Set build type if not set
set(default_build_type "Release")
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE ${default_build_type})
endif()

if(${UNIX})
    set(Boost_INCLUDE_DIR /usr/local/src/boost_1_70_0)
    set(Boost_LIBRARY_DIR /usr/local/src/boost_1_70_0/stage/lib)
else()
    set(Boost_INCLUDE_DIR C:/boost_1.70.0)
    set(Boost_LIBRARY_DIR C:/boost_1.70.0/stage/v140/x64/lib)
endif()

# find_package(Boost COMPONENTS chrono system filesystem REQUIRED)
# find_package(Boost REQUIRED)
find_package(Boost 1.70.0 REQUIRED)
include_directories(${Boost_INCLUDE_DIR})
link_directories(${Boost_LIBRARY_DIR})

include_directories("${CMAKE_SOURCE_DIR}/include")

set(TEST_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/src/Source.cpp
)

add_executable(BoostTest ${TEST_SOURCES})
target_link_libraries(BoostTest ${BOOST_LIBRARIES})