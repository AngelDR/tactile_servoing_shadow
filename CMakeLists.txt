cmake_minimum_required(VERSION 2.8.3)
project(tactile_servoing_shadow)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED
  roscpp rospy
  std_msgs message_generation
  pr2_controllers_msgs control_toolbox
  tf tf2 tf2_ros
  moveit_core moveit_ros_planning moveit_ros_planning_interface pluginlib cmake_modules
  )
  
  
find_package(Boost REQUIRED system filesystem date_time thread)

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)


## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

################################################
## Declare ROS messages, services and actions ##
################################################

## To declare and build messages, services or actions from within this
## package, follow these steps:
## * Let MSG_DEP_SET be the set of packages whose message types you use in
##   your messages/services/actions (e.g. std_msgs, actionlib_msgs, ...).
## * In the file package.xml:
##   * add a build_depend and a run_depend tag for each package in MSG_DEP_SET
##   * If MSG_DEP_SET isn't empty the following dependencies might have been
##     pulled in transitively but can be declared for certainty nonetheless:
##     * add a build_depend tag for "message_generation"
##     * add a run_depend tag for "message_runtime"
## * In this file (CMakeLists.txt):
##   * add "message_generation" and every package in MSG_DEP_SET to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * add "message_runtime" and every package in MSG_DEP_SET to
##     catkin_package(CATKIN_DEPENDS ...)
##   * uncomment the add_*_files sections below as needed
##     and list every .msg/.srv/.action file to be processed
##   * uncomment the generate_messages entry below
##   * add every package in MSG_DEP_SET to generate_messages(DEPENDENCIES ...)

## Generate messages in the 'msg' folder

## Generate services in the 'srv' folder

## Generate actions in the 'action' folder
# add_action_files(
#   FILES
#   Action1.action
#   Action2.action
# )

## Generate added messages and services with any dependencies listed here

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if you package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES pr2_moveit_tutorials
  CATKIN_DEPENDS 
    pr2_controller_manager  pr2_mechanism_msgs
    moveit_core moveit_ros_planning_interface
    tf2 tf2_ros
    std_msgs message_runtime
)
find_package(Eigen REQUIRED)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)
include_directories(SYSTEM ${Boost_INCLUDE_DIR} ${EIGEN_INCLUDE_DIRS})
include_directories(${catkin_INCLUDE_DIRS})
link_directories(${catkin_LIBRARY_DIRS})

## Declare a cpp library
# add_library(tactile_servoing_shadow
#   src/${PROJECT_NAME}/tactile_servoing_shadow.cpp
# )

## Declare a cpp executable
# add_executable(tactile_servoing_shadow_node src/tactile_servoing_shadow_node.cpp)
#add_executable(tactile_servo src/tactile_servoing.cpp)
add_executable(tactile_servo_hand src/tactile_servoing_hand.cpp)
add_executable(tactile_servo_node src/tactile_servo_node.cpp)
add_executable(tactile_servo_hand_biotac_gaussian src/tactile_servoing_hand_biotac.cpp)
add_executable(tactile_servo_hand_biotac_position src/tactile_servoing_hand_biotac_position.cpp)


#add_executable(finger_jacobian_service src/finger_jacobian_service.cpp)
#add_executable(sensor_tf_broadcaster src/sensor_tf_broadcaster.cpp)



## Add cmake target dependencies of the executable/library
## as an example, message headers may need to be generated before nodes
# add_dependencies(tactile_servoing_shadow_node tactile_servoing_shadow_generate_messages_cpp)

## Specify libraries to link a library or executable target against
# target_link_libraries(tactile_servoing_shadow_node
#   ${catkin_LIBRARIES}
# )
#target_link_libraries(tactile_servo ${catkin_LIBRARIES} ${Boost_LIBRARIES})
target_link_libraries(tactile_servo_hand ${catkin_LIBRARIES} ${Boost_LIBRARIES})
target_link_libraries(tactile_servo_node ${catkin_LIBRARIES} ${Boost_LIBRARIES})
target_link_libraries(tactile_servo_hand_biotac_gaussian ${catkin_LIBRARIES} ${Boost_LIBRARIES})
target_link_libraries(tactile_servo_hand_biotac_position ${catkin_LIBRARIES} ${Boost_LIBRARIES})

#target_link_libraries(sensor_tf_broadcaster ${catkin_LIBRARIES})
#target_link_libraries(finger_jacobian_service ${catkin_LIBRARIES})


#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
# install(TARGETS tactile_servoing_shadow tactile_servoing_shadow_node
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#install(TARGETS tactile_servo DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
install(TARGETS tactile_servo_hand DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
install(TARGETS tactile_servo_node DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
install(TARGETS tactile_servo_hand_biotac_gaussian DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
install(TARGETS tactile_servo_hand_biotac_position DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})


#install(TARGETS sensor_tf_broadcaster DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
#install(TARGETS finger_jacobian_service DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})


install(DIRECTORY launch DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_tactile_servoing_shadow.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
