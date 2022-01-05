cmake_minimum_required(VERSION 3.13)
# cmake_minimum_required(VERSION 3.12)

project(CMGDB)

# set(Boost_USE_STATIC_LIBS ON)

cmake_policy(SET CMP0054 NEW)
cmake_policy(SET CMP0127 NEW)

# Visual Studio C++ does not support keywords such
# as "and", "not", etc. Settting the /permissive-
# flag for the compiler makes it suppor them.
if(MSVC)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /permissive-")
endif()

if(APPLE)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -stdlib=libc++")
endif(APPLE)

add_subdirectory(pybind11)

# set(BOOST_ROOT "/home/runner/work/CMGDB_temp3/CMGDB_temp3/boost/boost")
# set(BOOST_INCLUDEDIR "/home/runner/work/CMGDB_temp3/CMGDB_temp3/boost/boost/include")

# set(BOOST_ROOT "/usr")
# set(BOOST_INCLUDEDIR "/usr/include")
set(BOOST_INCLUDEDIR "/usr/local/include")

message("Debug:")
message("BOOST_ROOT IS ${BOOST_ROOT}")
message("Boost_INCLUDE_DIR IS ${Boost_INCLUDE_DIR}")
message("Boost_LIBRARIES IS ${Boost_LIBRARIES}")

set(Boost_ARCHITECTURE "-x64")

find_package(Boost COMPONENTS chrono thread serialization REQUIRED)

message("Debug:")
message("BOOST_ROOT IS ${BOOST_ROOT}")
message("Boost_INCLUDE_DIR IS ${Boost_INCLUDE_DIR}")
message("Boost_LIBRARIES IS ${Boost_LIBRARIES}")

# CMAKE_TOOLCHAIN_FILE=C:/vcpkg/scripts/buildsystems/vcpkg.cmake
# find_package(gmp REQUIRED)

include_directories(${Boost_INCLUDE_DIRS})

if(Boost_FOUND)
  message(STATUS "Success!")
endif()

include_directories (
  /usr/local/include
  ${Boost_INCLUDE_DIR}
  ${CMAKE_SOURCE_DIR}/include
  ${USER_INCLUDE_PATH}/database
  ${USER_INCLUDE_PATH} )

link_directories (
  /usr/local/lib
  ${USER_LIBRARY_PATH} )

pybind11_add_module(_cmgdb src/CMGDB/_cmgdb/CMGDB.cpp)

# target_link_libraries(_cmgdb PRIVATE Boost::chrono Boost::thread Boost::serialization sdsl)

# target_link_libraries (
#   _cmgdb PRIVATE
#   Boost::chrono
#   Boost::thread
#   Boost::serialization
#   sdsl )

# add_executable(test src/main.cpp)

# target_link_libraries(test ${Boost_LIBRARIES})

# target_compile_definitions(test PRIVATE -DBOOST_NO_AUTO_PTR -DBOOST_ALL_NO_LIB)
