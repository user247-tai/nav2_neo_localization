cmake_minimum_required(VERSION 3.5)
project(nav2_neo_localization)

find_package(ament_cmake REQUIRED)
find_package(nav_msgs REQUIRED)
find_package(nav2_common REQUIRED)
find_package(nav2_util REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_components REQUIRED)
find_package(rclcpp_lifecycle REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(tf2 REQUIRED)
find_package(tf2_eigen REQUIRED)
find_package(tf2_ros REQUIRED)
find_package(tf2_sensor_msgs REQUIRED)
find_package(tf2_geometry_msgs REQUIRED)
find_package(ament_cmake REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(angles REQUIRED)
find_package(std_srvs REQUIRED)
find_package(pluginlib REQUIRED)

nav2_package()

include_directories(
  include
)

set(executable_name neo_localization)
set(library_name ${executable_name}_core)

set(dependencies
  rclcpp
  rclcpp_lifecycle
  rclcpp_components
  geometry_msgs
  nav_msgs
  nav2_msgs
  nav2_util
  sensor_msgs
  std_srvs
  tf2
  tf2_ros
  tf2_sensor_msgs
  tf2_geometry_msgs
  tf2_eigen
  angles
  pluginlib
)

# Main library
add_library(${library_name} SHARED
  src/neo_localization_node.cpp
)
ament_target_dependencies(${library_name}
  ${dependencies}
)

# Main executable
add_executable(${executable_name}
  src/main.cpp
)
ament_target_dependencies(${executable_name}
  ${dependencies}
)
target_link_libraries(${executable_name} ${library_name})

rclcpp_components_register_nodes(${library_name} "nav2_neo_localization::NeoLocalizationNode")

install(
  TARGETS ${library_name}
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(TARGETS ${executable_name}
  RUNTIME DESTINATION lib/${PROJECT_NAME}
)

install(DIRECTORY include/
  DESTINATION include/
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
  find_package(ament_cmake_gtest REQUIRED)
  # add_subdirectory(test)
endif()

ament_export_include_directories(include)
ament_export_libraries(${library_name})
ament_export_dependencies(${dependencies})
ament_package()