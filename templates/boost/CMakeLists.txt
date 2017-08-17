cmake_minimum_required(VERSION 2.6)

## Define modules path first
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/../cmake-modules")

## Set build type before using project()
if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "RelWithDebInfo" CACHE STRING "Build type")
    message(STATUS "No build type selected, default to ${CMAKE_BUILD_TYPE}")
else()
    message(STATUS ${CMAKE_BUILD_TYPE})
endif()

## ----------

# project(helloworld C CXX)

## SETTING UP COMPILER AND LINKER FLAGS (don't use -ffast-math !)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x -Wclobbered -Wignored-qualifiers -Wmissing-field-initializers -Wsign-compare -Wtype-limits -Wuninitialized -Wno-unused-parameter -Wunused-but-set-parameter -Wno-comment -Wno-type-limits -Wno-strict-aliasing -Wno-unused-local-typedefs -Wno-deprecated-declarations")
add_definitions(-DNDEBUG -DBOOST_UBLAS_NDEBUG)

set(LIBRARY_OUTPUT_PATH "${CMAKE_SOURCE_DIR}/lib")

## Find libraries

## BOOST
find_package(Boost 1.53 COMPONENTS program_options thread system filesystem unit_test_framework REQUIRED)
## BOOST NUMERIC BINDINGS
# find_package(BoostNumericBindings REQUIRED)

## DEFINE DIRECTORIES AND FILES
include_directories(
  ${INCS}
  ${Boost_INCLUDE_DIR}
  ${BoostNumericBindings_INCLUDE_DIR}
)

link_directories(
  ~/usrlocal/lib
  ${Boost_LIBRARY_DIRS}
)

set(LIBS
  ${LIBS}
)

add_executable(hello
    src/main.cpp
)

target_link_libraries(hello ${LIBS})
