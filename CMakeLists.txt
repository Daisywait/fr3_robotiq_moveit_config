# 假设新的配置包名为 fr3_robotiq_moveit_config
cmake_minimum_required(VERSION 3.8)
project(fr3_robotiq_moveit_config) # [修改] 更新项目名称

# -------------------------------------------------------------------
# 查找依赖 (Find Packages) - 修复了缺失的依赖查找
# -------------------------------------------------------------------

find_package(ament_cmake REQUIRED)

# Franka 核心依赖 - 修复了 franka_robot_state_broadcaster 缺失的问题
find_package(franka_description REQUIRED)
find_package(franka_hardware REQUIRED)
find_package(franka_robot_state_broadcaster REQUIRED) # <--- 修复：确保找到这个包
find_package(franka_fr3_moveit_config REQUIRED)

# [关键新增] Robotiq 夹爪依赖
find_package(robotiq_description REQUIRED) 

# MoveIt 核心及插件依赖
find_package(moveit_core REQUIRED)
find_package(moveit_ros_move_group REQUIRED)
find_package(moveit_planners_ompl REQUIRED)
find_package(moveit_servo REQUIRED)
find_package(joint_trajectory_controller REQUIRED)
find_package(controller_manager REQUIRED)
find_package(robot_state_publisher REQUIRED)
find_package(xacro REQUIRED)

# -------------------------------------------------------------------
# 安装文件 (Install Files) - 沿用您选择的目录安装方式
# -------------------------------------------------------------------

install(
  DIRECTORY config launch rviz
  DESTINATION share/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
