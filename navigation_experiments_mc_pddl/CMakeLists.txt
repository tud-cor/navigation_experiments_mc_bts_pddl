cmake_minimum_required(VERSION 3.5)
project(navigation_experiments_mc_pddl)


find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_action REQUIRED)
find_package(plansys2_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(nav2_msgs REQUIRED)
find_package(mros2_msgs REQUIRED)
find_package(std_srvs REQUIRED)
find_package(system_modes REQUIRED)
find_package(plansys2_executor REQUIRED)
find_package(plansys2_domain_expert REQUIRED)

set(CMAKE_CXX_STANDARD 17)

set(dependencies
    rclcpp
    rclcpp_action
    plansys2_msgs
    nav2_msgs
    plansys2_executor
    plansys2_problem_expert
    plansys2_domain_expert
    mros2_msgs
    std_srvs
    system_modes
)

add_executable(move_action_node src/move_action_node.cpp)
ament_target_dependencies(move_action_node ${dependencies})

add_executable(patrol_action_node src/patrol_action_node.cpp)
ament_target_dependencies(patrol_action_node ${dependencies})

add_executable(charge_action_node src/charge_action_node.cpp)
ament_target_dependencies(charge_action_node ${dependencies})

add_executable(ask_charge_action_node src/ask_charge_action_node.cpp)
ament_target_dependencies(ask_charge_action_node ${dependencies})

add_executable(degraded_move_action_node src/degraded_move_action_node.cpp)
ament_target_dependencies(degraded_move_action_node ${dependencies})

add_executable(reconfigure_action_node src/reconfigure_action_node.cpp)
ament_target_dependencies(reconfigure_action_node ${dependencies})

add_executable(recover_nav_sensor_node src/recover_nav_sensor_node.cpp)
ament_target_dependencies(recover_nav_sensor_node ${dependencies})

add_executable(patrolling_controller_node src/patrolling_controller_node.cpp)
ament_target_dependencies(patrolling_controller_node ${dependencies})

add_executable(patrolling_reconfig_controller_node src/patrolling_reconfig_controller_node.cpp)
ament_target_dependencies(patrolling_reconfig_controller_node ${dependencies})

install(DIRECTORY launch pddl DESTINATION share/${PROJECT_NAME})

install(TARGETS
  move_action_node
  patrol_action_node
  charge_action_node
  ask_charge_action_node
  degraded_move_action_node
  reconfigure_action_node
  recover_nav_sensor_node
  patrolling_controller_node
  patrolling_reconfig_controller_node
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION lib/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()

  find_package(ament_cmake_gtest REQUIRED)
endif()

ament_export_dependencies(${dependencies})

ament_package()