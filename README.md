1. Getting Started
   Prerequisites

Ubuntu 22.04 LTS

ROS 2 Humble Hawksbill
ROS 2 Installation Guide

colcon build tools

sudo apt install python3-colcon-common-extensions


Python libraries

python3 -m pip install numpy scipy matplotlib


Optional: turtlesim or turtlebot3 + gazebo for simulation

sudo apt install ros-humble-turtlesim ros-humble-turtlebot3* ros-humble-gazebo-ros-pkgs

Workspace Setup

Create a workspace named projectai and clone your repo:

# create workspace and enter
mkdir -p ~/projectai/src
cd ~/projectai/src

# clone (example)
git clone https://github.com/<your-username>/projectai.git .


If you start from scratch:

ros2 pkg create --build-type ament_python path_smoothing --dependencies rclpy nav_msgs geometry_msgs std_msgs
ros2 pkg create --build-type ament_python trajectory_generation --dependencies rclpy nav_msgs geometry_msgs std_msgs
ros2 pkg create --build-type ament_python trajectory_controller --dependencies rclpy geometry_msgs nav_msgs tf2_ros
ros2 pkg create --build-type ament_python sim_bridge --dependencies rclpy nav_msgs geometry_

3. Build & Source
cd ~/projectai
source /opt/ros/humble/setup.bash
colcon build --symlink-install
source install/setup.bash

Run with TurtleBot3 + Gazebo

Launch simulation:

export TURTLEBOT3_MODEL=burger
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py

Testing & Evaluation
Unit Tests

Run with:

colcon test --packages-select path_smoothing trajectory_generation trajectory_controller

Parameters & Tuning
Parameter	Meaning	Typical Value
v_max	Maximum linear velocity	0.25 m/s
a_max	Max acceleration	0.5 m/s²
lookahead_distance	Pure Pursuit look-ahead	0.3–0.6 m
dt	Control loop period	0.05 s

Credits

Developed by Tharun M.T K
Part of the Robotics Navigation Assignment (Path Smoothing & Trajectory Control).

Libraries used:

ROS 2 Humble

NumPy, SciPy, Matplotlib

geometry_msgs, nav_msgs, tf2_ros
