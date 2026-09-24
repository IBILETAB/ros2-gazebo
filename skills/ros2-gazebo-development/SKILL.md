---
name: ros2-gazebo-development
description: Create, modify, and debug ROS 2 robotics software in Python and connect it to Gazebo simulations. Use for rclpy nodes, ament_python packages, ROS 2 launch files, Gazebo worlds and models, ros_gz integration, topic bridges, simulated sensors, and ROS-Gazebo troubleshooting.
---

# ROS 2 Python and Gazebo Development

Help the user build a working ROS 2 Python system and integrate it with their Gazebo simulation. Make version assumptions explicit and keep examples consistent with the user's installed ROS distribution and Gazebo generation.

## Start by identifying the environment

- Inspect the repository before changing it. Respect existing package names, conventions, and uncommitted work.
- Determine the ROS 2 distribution, OS, Python version, and Gazebo generation/version from the project or user. Ask only for details that materially affect the implementation; otherwise state a reasonable assumption.
- Distinguish modern Gazebo (formerly Ignition; packages and commands commonly use `gz` and `ros_gz`) from Gazebo Classic (`gazebo` and `gazebo_ros`). Do not mix their plugin names, launch commands, or bridge configuration.
- Prefer the integration already present in the repository. Do not upgrade or migrate a project to another Gazebo generation unless asked.
- Use official ROS 2 and Gazebo documentation when exact API, package, or compatibility details are uncertain. Do not invent package names, message types, plugin filenames, or CLI flags.

## Implement ROS 2 Python packages

- Follow the repository's existing ROS build type. For a new pure Python ROS 2 package, use `ament_python` conventions: `package.xml`, `setup.py`, `setup.cfg`, a Python package directory, and a `resource/<package_name>` marker.
- Use `rclpy` nodes with clear publishers, subscriptions, services, actions, parameters, and timers. Choose standard message types when they fit; define custom interfaces only when needed.
- Make node names, topic names, frames, QoS, and units explicit. Use parameters for values users are likely to tune.
- Keep callbacks short and avoid blocking sleeps or long-running work in executor callbacks. Handle shutdown and resource cleanup cleanly.
- Add or update launch files when multiple nodes, parameter files, remappings, namespaces, or simulator processes need coordinated startup.

## Integrate with Gazebo

- Identify whether the feature belongs in ROS, the simulator, or both. Keep robot behavior in ROS nodes where practical; use simulator plugins for simulation-specific systems and hardware-like interfaces.
- For modern Gazebo, investigate the matching `ros_gz` packages, such as `ros_gz_sim` and `ros_gz_bridge`, that are compatible with the ROS distribution and Gazebo release in use. For Gazebo Classic, follow the project's `gazebo_ros_pkgs` setup.
- Bridge only the topics needed across ROS and Gazebo. Check message type conversion, direction, topic names, QoS, namespaces, and simulation time. Use `/clock` and enable simulated time for ROS nodes when appropriate.
- Confirm model and world resources resolve correctly, including model paths, plugin libraries, meshes, and environment variables. Keep resource paths portable where possible.
- Do not assume a bridge automatically provides a ROS interface for every Gazebo transport message or simulator feature. Verify the exact supported conversion and plugin.

## Build, run, and debug

Give commands for the user's shell and ROS distribution. A typical colcon workflow is:

```bash
source /opt/ros/<distro>/setup.bash
cd <workspace>
rosdep install --from-paths src --ignore-src -r -y
colcon build --symlink-install
source install/setup.bash
```

Treat this as a template: omit or adapt dependency installation when the environment is offline, already provisioned, or uses another OS. For Windows, explain the supported ROS 2 setup rather than assuming the Linux paths above.

When debugging, check in this order:

1. Build output and package dependencies.
2. Simulator startup, world/model loading, and plugin errors.
3. ROS node and launch logs.
4. ROS graph and topic visibility (`ros2 node list`, `ros2 topic list`, `ros2 topic info`).
5. Gazebo Transport topics and bridge direction/type configuration.
6. Time, QoS, namespace, frame IDs, and message type compatibility.

Prefer a small reproducible change and explain which files and commands are involved. Do not claim the system runs unless it was actually run in a compatible ROS/Gazebo environment. Do not add or run tests unless the user asks.
