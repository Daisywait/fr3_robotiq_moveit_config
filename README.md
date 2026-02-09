# fr3_robotiq_moveit_config (jazzy 分支)

本分支基于官方 `franka_ros2` 仓库 **jazzy** 分支的 `franka_fr3_moveit_config`。
以下是相较官方配置包的主要改动点：

## 1) 夹爪替换：Franka Hand → Robotiq 2F-85
- URDF/SRDF 改为 `fr3_robotiq.urdf.xacro` 与 `fr3_robotiq.srdf.xacro`
- 引入 `robotiq_description` 并将末端 `ee_id` 固定为 `robotiq_gripper`
- 新增 `use_gripper` Xacro 参数，允许 arm-only 启动时不加载夹爪硬件
- 新增 `gripper_reactivate_on_startup` Xacro 参数，用于控制启动时是否自动激活/标定夹爪

## 2) MoveIt 控制器配置
- `fr3_robotiq_controllers.yaml` 使用 `robotiq_gripper_controller`
- 夹爪控制由 `FollowJointTrajectory` 驱动，关节为 `robotiq_85_left_knuckle_joint`

## 3) ros2_control 控制器配置
- 新增 `robotiq_gripper_controller`
- 新增 `fr3_velocity_controller`（速度控制）
- 继承 jazzy 的控制器管理器参数：`thread_priority` / `enable_overrun`

## 4) 规划与运动学配置
- 规划组名称调整为 `fr3_arm` / `fr3_arm_gripper`
- 运动学求解器对齐 jazzy：`kdl_kinematics_plugin/KDLKinematicsPlugin`
- 新增 `fr3_robotiq_joint_limits.yaml`（对应 jazzy 新增的 joint limits）

## 5) Launch 文件对齐 jazzy 结构
- 引入 joint limits 与新的 request/response adapters
- 使用本包的 `fr3_robotiq_*` 配置文件
- 使用 Robotiq 的 URDF/SRDF

## 6) 启动方式说明
- 仅保留一键启动 `fr3_robotiq_servo.launch.py`
- 夹爪默认自动激活并标定
