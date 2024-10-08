# DRIMS2 Simulation Environment

## Gazebo Simulation

In order to run the simulation:

1. Load robot controllers
```bash
roslaunch abb_wrapper_control launchControlServer.launch
```

2. Load task server
```bash
roslaunch abb_wrapper_control launchTaskServer.launch
```

3. Load Gazebo environment
```bash
roslaunch drims_dice_demo arm_gazebo.launch robot:=yumi # or robot:=gofa
```


4. Load dice
```bash
roslaunch drims_dice_demo spawn_dice.launch
```

**NOTE:** Each command should run in its own terminal

## Example nodes

Two example nodes are provided in both Python and C++.

To launch them:

```bash
rosrun DRIMS_template take_the_dice_example.py
```

for the **Python** version and,

```bash
roslaunch DRIMS_template test_example.launch
```

for the **C++** version.

For the **C++** version, a template to help starting is provided (`src/task_dice.cpp`).

Both of the example programs present a basic use of the services to move the robot:
- `/plan_and_execute_pose`: plan a collision-free joint trajectory and to a given a goal pose and execute it.

**Service structure `abb_wrapper_msgs/plan_and_execute_pose`**
```
# == Request ==
geometry_msgs/Pose goal_pose
bool is_relative
---
# == Response ==
bool success
string message
```

- `/plan_and_execute_joint`: plan a collision-free joint trajectory and to a given goal joints configuration and execute it.

**Service structure `abb_wrapper_msgs/plan_and_execute_joint`**
```
# == Request ==
float64[] joint_goal
---
# == Response ==
bool success
string message
```

- `/plan_and_execute_slerp`: plan a collision-free cartesian trajectory and to a given goal  and execute it.

**Service structure `abb_wrapper_msgs/plan_and_execute_slerp`**
```
# == Request ==
geometry_msgs/Pose goal_pose
bool is_relative
---
# == Response ==
bool success
string message
```

- `/open_gripper` and `/close_gripper`

**Service structure `abb_wrapper_msgs/open_gripper` and `abb_wrapper_msgs/open_gripper`**
```
bool in_flag
---
bool out_flag
string message
```