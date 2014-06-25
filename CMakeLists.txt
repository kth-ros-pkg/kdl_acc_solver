cmake_minimum_required(VERSION 2.8.3)
project(kdl_acc_solver)

find_package(orocos_kdl REQUIRED)
find_package(catkin REQUIRED COMPONENTS roscpp urdf)

include_directories(include ${orocos_kdl_INCLUDE_DIRS} ${catkin_INCLUDE_DIRS})

link_directories(${catkin_LIBRARY_DIRS})
link_directories(${orocos_kdl_LIBRARY_DIRS})

find_library(KDL_LIBRARY REQUIRED NAMES orocos-kdl HINTS ${orocos_kdl_LIBRARY_DIRS})

catkin_package(
  DEPENDS orocos_kdl
  CATKIN_DEPENDS urdf
  INCLUDE_DIRS include
  LIBRARIES chainfksolveracc_recursive
)


add_library(chainfksolveracc_recursive src/chainfksolveracc_recursive.cpp)
target_link_libraries(chainfksolveracc_recursive ${catkin_LIBRARIES} ${orocos_kdl_LIBRARIES})

install(TARGETS chainfksolveracc_recursive
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
