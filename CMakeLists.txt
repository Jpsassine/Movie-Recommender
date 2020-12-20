CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

ADD_SUBDIRECTORY(googletest)

SET(CMAKE_CXX_STANDARD_11)
set(Boost_INCLUDE_DIR /usr/local/include/boost)
set(Boost_LIBRARY_DIR /usr/local/src/boost/stage/lib)
find_package(Boost COMPONENTS system filesystem REQUIRED)
include_directories(${Boost_INCLUDE_DIR})
link_directories(${Boost_LIBRARY_DIR})
list( APPEND CMAKE_CXX_FLAGS "-std=c++0x ${CMAKE_CXX_FLAGS} -g -ftest-coverage -fprofile-arcs")




ADD_EXECUTABLE(movieRec
main.cpp
MediaStructure.cpp
DisplayStrategy.cpp
DataParser.cpp
Movie.cpp

)

ADD_EXECUTABLE(test
unit_test.cpp

MediaStructure.cpp
DisplayStrategy.cpp
DataParser.cpp
Movie.cpp
)

TARGET_LINK_LIBRARIES(test gtest)
TARGET_LINK_LIBRARIES( test  LINK_PUBLIC ${Boost_LIBRARIES} )
TARGET_LINK_LIBRARIES( movieRec  LINK_PUBLIC ${Boost_LIBRARIES} )
TARGET_COMPILE_DEFINITIONS(test PRIVATE gtest_disable_pthreads=ON)