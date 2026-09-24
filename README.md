# ROS 2 + Gazebo Codex Plugin

A Codex plugin with practical guidance for building ROS 2 robotics software in Python and integrating it with Gazebo simulations.

## What it helps with

- Creating and maintaining `ament_python` ROS 2 packages and `rclpy` nodes
- Writing launch files and coordinating nodes with simulator processes
- Connecting ROS 2 to modern Gazebo with `ros_gz`, or to Gazebo Classic with `gazebo_ros`
- Debugging topics, bridges, simulated time, QoS, namespaces, frames, and model resources

The included skill is version-aware. It asks Codex to identify the project's ROS 2 distribution and Gazebo generation before suggesting commands or plugin configuration.

## Install with Codex CLI

```bash
codex plugin marketplace add IBILETAB/ros2-gazebo
codex plugin add ros2-gazebo@ros2-gazebo-marketplace
```

Then start a new Codex task so it loads the plugin's skill.

## Development

The skill source is `skills/ros2-gazebo-development/SKILL.md`; plugin metadata is in `.codex-plugin/plugin.json`.

## License

No license has been specified yet.
