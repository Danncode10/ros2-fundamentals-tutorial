# Lesson 2 Python Node Minimal Code First Cheat Sheet

## Main Idea

Create one Python node, register it in `setup.py`, build, run, and prove it is alive.

## File Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `cd ~/ros2_ws` | Move to the workspace root. | Before checking or building. | `pwd` ends in `ros2_ws`. |
| `ls src/rover_core` | Show the package folder contents. | Checking Lesson 1 is ready. | You see `package.xml` and `setup.py`. |
| `cd ~/ros2_ws/src/rover_core/rover_core` | Move into the Python module folder. | Before creating the node file. | You are inside the inner `rover_core` folder. |
| `nano rover_heartbeat_minimal.py` | Open/create the Python node file. | Writing the heartbeat node. | File saves successfully. |
| `cd ~/ros2_ws/src/rover_core && nano setup.py` | Open the package setup file. | Registering the node command. | Console script line is added. |

## Build And Run Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `colcon build --packages-select rover_core` | Build only the `rover_core` package. | After editing node code or `setup.py`. | `Finished <<< rover_core`. |
| `source install/setup.bash` | Refresh this terminal with the built package. | After every build. | No error; usually no output. |
| `ros2 run rover_core rover_heartbeat_minimal` | Run the registered heartbeat node. | Starting the node. | Heartbeat logs repeat. |
| `ros2 node list` | Ask ROS 2 which nodes are alive. | Verifying from another terminal. | `/rover_heartbeat_minimal` appears. |
| `ros2 node info /rover_heartbeat_minimal` | Ask ROS 2 for details about that node. | Inspecting the live node. | Node information prints. |

## Setup.py Line

```python
'rover_heartbeat_minimal = rover_core.rover_heartbeat_minimal:main',
```

- This means: command name = Python file path + `main()` function.

## Tiny Terms

| Term | Meaning |
|---|---|
| Node | Running ROS 2 program. |
| `rclpy` | Python library for ROS 2 nodes. |
| Logger | ROS 2-friendly print. |
| Spin | Keeps a node alive and processing. |
| Console script | Command that `ros2 run` can start. |

## Remember

- Workflow: create file, register, build, source, run, verify.
- Package = `rover_core`; node = `rover_heartbeat_minimal`.
- If `ros2 run` fails, check `setup.py`, rebuild, and source again.
