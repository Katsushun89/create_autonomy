cmake_minimum_required(VERSION 3.5)
project(ca_driver)

if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

find_package(ament_cmake REQUIRED)
find_package(ca_msgs REQUIRED)
find_package(diagnostic_msgs REQUIRED)
# find_package(diagnostic_updater REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(libcreate REQUIRED)
find_package(nav_msgs REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_lifecycle REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(std_msgs REQUIRED)
find_package(tf2 REQUIRED)
find_package(tf2_ros REQUIRED)

include_directories(
  include
  ${ca_msgs_INCLUDE_DIRS}
  ${diagnostic_msgs_INCLUDE_DIRS}
  # ${diagnostic_updater_INCLUDE_DIRS}
  ${geometry_msgs_INCLUDE_DIRS}
  ${libcreate_INCLUDE_DIRS}
  ${nav_msgs_INCLUDE_DIRS}
  ${rclcpp_INCLUDE_DIRS}
  ${sensor_msgs_INCLUDE_DIRS}
  ${std_msgs_INCLUDE_DIRS}
  ${tf2_INCLUDE_DIRS}
)

add_executable(${PROJECT_NAME} src/create_driver.cpp)
ament_target_dependencies(${PROJECT_NAME}
 "ca_msgs"
 "diagnostic_msgs"
 # diagnostic_updater"
 "geometry_msgs"
 "libcreate"
 "nav_msgs"
 "rclcpp"
 "rclcpp_lifecycle"
 "sensor_msgs"
 "std_msgs"
 "tf2"
 "tf2_ros"
)

#Test 
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

#lib directory
install(TARGETS ${PROJECT_NAME}
  DESTINATION lib/${PROJECT_NAME}
)

#include directory
install(DIRECTORY include/${PROJECT_NAME}
  DESTINATION include/${PROJECT_NAME}
  FILES_MATCHING PATTERN "*.hpp"
)

#config directory
install(DIRECTORY
  config
  DESTINATION share/${PROJECT_NAME}/
)

install(DIRECTORY
  launch
  DESTINATION share/${PROJECT_NAME}/
)

ament_package()