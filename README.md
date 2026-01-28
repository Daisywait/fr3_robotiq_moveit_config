# fr3_robotiq_moveit_config (humble 分支)

本分支基于官方 `franka_ros2` 仓库 **humble** 分支的 `franka_fr3_moveit_config`。
以下是相较官方配置包的主要改动点：

## 1) 夹爪替换：Franka Hand → Robotiq 2F-85
- URDF/SRDF 改为 `fr3_robotiq.urdf.xacro` 与 `fr3_robotiq.srdf.xacro`
- 引入 `robotiq_description` 并将末端 `ee_id` 固定为 `robotiq_gripper`

## 2) MoveIt 控制器配置
- `fr3_robotiq_controllers.yaml` 使用 `robotiq_gripper_controller`
- 夹爪控制由 `FollowJointTrajectory` 驱动，关节为 `robotiq_85_left_knuckle_joint`

## 3) ros2_control 控制器配置
- 新增 `robotiq_gripper_controller`
- 新增 `fr3_velocity_controller`（速度控制）

## 4) 运动学配置
- 使用 `fr3_robotiq_kinematics.yaml`，求解器为 LMA
