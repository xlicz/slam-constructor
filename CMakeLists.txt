cmake_minimum_required(VERSION 2.8.3)
SET(CMAKE_CXX_FLAGS "-std=c++14 -Wall -O3 -pthread -fdiagnostics-color")
project(slam_fmwk)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs
  sensor_msgs
  nav_msgs
  geometry_msgs
  tf
  message_filters
  rosbag_storage
)

find_package(GTest)

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)

################################################
## Declare ROS messages, services and actions ##
################################################

## To declare and build messages, services or actions from within this
## package, follow these steps:
## * Let MSG_DEP_SET be the set of packages whose message types you use in
##   your messages/services/actions (e.g. std_msgs, actionlib_msgs, ...).
## * In the file package.xml:
##   * add a build_depend tag for "message_generation"
##   * add a build_depend and a run_depend tag for each package in MSG_DEP_SET
##   * If MSG_DEP_SET isn't empty the following dependency has been pulled in
##     but can be declared for certainty nonetheless:
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
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate actions in the 'action' folder
# add_action_files(
#   FILES
#   Action1.action
#   Action2.action
# )

## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   std_msgs
# )

################################################
## Declare ROS dynamic reconfigure parameters ##
################################################

## To declare and build dynamic reconfigure parameters within this
## package, follow these steps:
## * In the file package.xml:
##   * add a build_depend and a run_depend tag for "dynamic_reconfigure"
## * In this file (CMakeLists.txt):
##   * add "dynamic_reconfigure" to
##     find_package(catkin REQUIRED COMPONENTS ...)
##   * uncomment the "generate_dynamic_reconfigure_options" section below
##     and list every .cfg file to be processed

## Generate dynamic reconfigure parameters in the 'cfg' folder
# generate_dynamic_reconfigure_options(
#   cfg/DynReconf1.cfg
#   cfg/DynReconf2.cfg
# )

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
#  LIBRARIES slam_fmwk
#  CATKIN_DEPENDS roscpp std_msgs tf
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)
include_directories(
  ${catkin_INCLUDE_DIRS}
  ${GTEST_INCLUDE_DIRS}
)

## Declare a C++ library
# add_library(slam_fmwk
#   src/${PROJECT_NAME}/slam_fmwk.cpp
# )

## Add cmake target dependencies of the library
## as an example, code may need to be generated before libraries
## either from message generation or dynamic reconfigure
# add_dependencies(slam_fmwk ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Declare a C++ executable

add_executable(wg_pr2_bag_adapter src/ros/wg_pr2_bag_adapter.cpp)
add_executable(lslam2D_bag_runner src/ros/lslam2D_bag_runner.cpp)
add_executable(gmapping src/slams/gmapping/gmapping.cpp)
add_executable(tiny_slam src/slams/tiny/tiny_slam.cpp)
add_executable(viny_slam src/slams/viny/viny_slam.cpp)
add_executable(viny_slam_x src/slams/vinyx/vinyx_slam.cpp)
add_executable(path_publisher src/ros/path_publisher.cpp)
add_executable(p2D_ss_evaluator src/utils/pose2D_search_space_evaluator.cpp)

## Add cmake target dependencies of the executable
## same as for the library above
# add_dependencies(slam_fmwk_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Specify libraries to link a library or executable target against

target_link_libraries(wg_pr2_bag_adapter ${catkin_LIBRARIES})
target_link_libraries(lslam2D_bag_runner ${catkin_LIBRARIES})
target_link_libraries(gmapping ${catkin_LIBRARIES})
target_link_libraries(tiny_slam ${catkin_LIBRARIES})
target_link_libraries(viny_slam ${catkin_LIBRARIES})
target_link_libraries(viny_slam_x ${catkin_LIBRARIES})
target_link_libraries(path_publisher ${catkin_LIBRARIES})

#target_link_libraries(openratslam_odom_converter ${catkin_LIBRARIES})
#target_link_libraries(scan_dbg
#   ${catkin_LIBRARIES}
#)

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
# install(TARGETS slam_fmwk slam_fmwk_node
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

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_slam_fmwk.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

# Maps
catkin_add_gtest(area_occupancy_estimator-test
                 test/core/maps/area_occupancy_estimator_test.cpp)
catkin_add_gtest(gm_scan_adders-test
                 test/core/maps/grid_map_scan_adders_test.cpp)
catkin_add_gtest(unbounded_plain_grid_map-test
                 test/core/maps/unbounded_plain_grid_map_test.cpp)
catkin_add_gtest(unbounded_lazy_tiled_grid_maps-test
                 test/core/maps/unbounded_lazy_tiled_grid_map_test.cpp)
catkin_add_gtest(regular_squares_grid-test
                 test/core/maps/regular_squares_grid_test.cpp)
catkin_add_gtest(grid_rasterization-test
                 test/core/maps/grid_rasterization_test.cpp)
catkin_add_gtest(rescalable_caching_grid_map-test
                 test/core/maps/rescalable_caching_grid_map_test.cpp)

# Core common
catkin_add_gtest(trig_utils-test
                 test/core/trigonometry_utils_test.cpp)
catkin_add_gtest(lwrectangle-test
                 test/core/light_weight_rectangle_test.cpp)
catkin_add_gtest(geom_dprimitives-test
                 test/core/geometry_discrete_primitives_test.cpp)

# Core states
catkin_add_gtest(sensor_data-test
                 test/core/states/sensor_data_test.cpp)

# Features
catkin_add_gtest(angle_histogram-test
                 test/core/features/angle_histogram_test.cpp)

# Scan Matching
catkin_add_gtest(occupancy_observation_probability-test
  test/core/scan_matchers/occupancy_observation_probability_test.cpp)
catkin_add_gtest(hill_climbing_sm-smoke_test
                 test/core/scan_matchers/hill_climbing_sm_smoke_test.cpp)
catkin_add_gtest(brute_force_sm-smoke_test
                 test/core/scan_matchers/brute_force_sm_smoke_test.cpp)

catkin_add_gtest(bfmrsm-smoke_test
                 test/core/scan_matchers/bf_multi_res_sm_smoke_test.cpp)

# Utils common
catkin_add_gtest(grid_map_patcher-test
                 test/utils/data_generation/grid_map_patcher_test.cpp)
catkin_add_gtest(map_primitives-test
                 test/utils/data_generation/map_primitives_test.cpp)

catkin_add_gtest(lscan_generator-test
                 test/utils/data_generation/laser_scan_generator_test.cpp)

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
