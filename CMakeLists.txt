cmake_minimum_required(VERSION 2.4.6)
project(ompl_planner_base)

#set(ROS_BUILD_TYPE RelWithDebInfo)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  pluginlib
  nav_core
  control_msgs
  costmap_2d
  geometry_msgs
  nav_msgs
  tf
  base_local_planner
  angles
)


#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

## Generate messages in the 'msg' folder
add_message_files(
   FILES
   OMPLPlannerBaseStats.msg
   OMPLPlannerDiagnostics.msg
)

generate_messages(
   DEPENDENCIES
   geometry_msgs
)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ompl_planner_base
  CATKIN_DEPENDS
  DEPENDS
)

include_directories(include
  ${catkin_INCLUDE_DIRS}
)



# build the library
add_library(ompl_planner_base src/ompl_planner_base.cpp)
target_link_libraries(ompl_planner_base
  ${catkin_LIBRARIES}
)

# build evaluation node as executable
add_executable(eval_ompl_plugin_node src/eval_ompl_plugin.cpp)
target_link_libraries(eval_ompl_plugin_node
  ${catkin_LIBRARIES}
)
