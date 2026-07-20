# Phase 2 Lesson 2 Python Node Minimal Code First Cheat Sheet

## Big Picture

- A **node** is a running ROS 2 program with one focused job.
- The node code lives in the package, but `setup.py` registers the command that `ros2 run` can start.
- Beginner workflow: create node file, register, build, source, run, verify.

## Must Remember

- `rover_core` is the package; `rover_heartbeat_minimal` is the node.
- `rclpy.init()` starts ROS 2 support for Python code.
- `rclpy.create_node("name")` creates the node ROS 2 can see.
- `node.get_logger().info(...)` prints ROS 2-style log messages.
- `setup.py` connects a short command name to the Python `main()` function.
- After building, source `install/setup.bash` in every terminal that needs the workspace.

## Key Words

| Word | Quick meaning |
|---|---|
| Node | Running ROS 2 program with one focused job |
| Package | Folder that organizes related ROS 2 code and metadata |
| `rclpy` | Python library for writing ROS 2 nodes |
| `init` | Starts ROS 2 support for the Python program |
| Logger | ROS 2-friendly way to print messages |
| Spin | Lets ROS 2 keep the node alive and process work |
| Shutdown | Cleanly stops ROS 2 support for the program |
| Console script | Registered command that `ros2 run` can start |
| `setup.py` | File that registers Python commands for the package |

## Tiny Diagram Or Mental Model

```text
node file -> setup.py entry -> colcon build -> source install/setup.bash -> ros2 run -> ros2 node list
```

Mental model:

```text
rover_heartbeat_minimal = rover_core.rover_heartbeat_minimal:main
command name             = Python file location             :function
```

## Commands To Recognize

```bash
cd ~/ros2_ws/src/rover_core/rover_core
nano rover_heartbeat_minimal.py
```

- Creates the Python node file inside the package's Python folder.

```bash
cd ~/ros2_ws/src/rover_core
nano setup.py
```

- Opens the file where the console script is registered.

```bash
colcon build
```

- Builds all packages in the workspace. Works here because the workspace has one package.

```bash
colcon build --packages-select rover_core
```

- Builds only `rover_core`; useful later when the workspace has many packages.

```bash
source install/setup.bash
```

- Teaches the current terminal about the newly built package commands.

```bash
ros2 run rover_core rover_heartbeat_minimal
```

- Runs the heartbeat node.

```bash
ros2 node list
```

- Verifies that ROS 2 can see the running node.

```bash
ros2 node info /rover_heartbeat_minimal
```

- Shows details about the running node.

## Quick Self-Check

- Can I explain the difference between a package and a node?
- Can I explain why `setup.py` is needed before `ros2 run` can find the node?
- Can I explain why I build and then source before running the node?
- Can I prove my node is alive with `ros2 node list`?
- Can I create a second node like `rover_status_beacon` using the same workflow?
