cmake_minimum_required(VERSION 3.0)
project(HoughForest)

find_package(OpenCV REQUIRED)

set(CMAKE_BUILD_TYPE Release)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(SOURCE_FILE CRForest-Detector.cpp CRForestDetector.cpp CRPatch.cpp CRTree.cpp HoG.cpp)
set(HEADER_FILE  CRForestDetector.h CRPatch.h CRTree.h HoG.h CRForest.h)

add_executable(HoughForest ${SOURCE_FILE} ${HEADER_FILE})

target_link_libraries(HoughForest ${OpenCV_LIBS})


