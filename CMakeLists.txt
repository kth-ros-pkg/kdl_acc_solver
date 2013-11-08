cmake_minimum_required(VERSION 2.8.3)
project(kdl_acc_solver)

find_package(catkin REQUIRED COMPONENTS roscpp orocos_kdl urdf)

catkin_package(
  DEPENDS 
  CATKIN_DEPENDS orocos_kdl urdf
  INCLUDE_DIRS include
  LIBRARIES chainfksolveracc_recursive
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

link_directories(${catkin_LIBRARY_DIRS})

add_library(chainfksolveracc_recursive src/chainfksolveracc_recursive.cpp)
target_link_libraries(chainfksolveracc_recursive ${catkin_LIBRARIES})

install(TARGETS chainfksolveracc_recursive
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
