cmake_minimum_required(VERSION 2.8.3)
project(vector_map)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  tf
  geometry_msgs
  visualization_msgs
  vector_map_msgs
)

set(CMAKE_CXX_FLAGS "-std=c++11 -O2 -Wall ${CMAKE_CXX_FLAGS}")

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES vector_map
  CATKIN_DEPENDS roscpp tf geometry_msgs visualization_msgs vector_map_msgs
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

add_library(vector_map lib/vector_map/vector_map.cpp)
add_dependencies(vector_map ${catkin_EXPORTED_TARGETS})

## Install executables and/or libraries
install(TARGETS vector_map
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})

## Install project namespaced headers
install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})
