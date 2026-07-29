# Lesson 2 Python Node Minimal Code First Cheat Sheet

## Lesson Reminder

Create one tiny Python node, register it in `setup.py`, build, run, and verify it is alive.

## Commands

```bash
echo $ROS_DISTRO
source /opt/ros/jazzy/setup.bash
cd ~/ros2_ws
ls src/rover_core
```

- Check ROS 2 and confirm the package exists.

```bash
cd ~/ros2_ws/src/rover_core/rover_core
nano rover_heartbeat_minimal.py
```

- Create the node file.

```bash
cd ~/ros2_ws/src/rover_core
nano setup.py
```

- Register the console script.

```python
'rover_heartbeat_minimal = rover_core.rover_heartbeat_minimal:main',
```

- Command name = Python module path + `main`.

```bash
cd ~/ros2_ws
colcon build --packages-select rover_core
source install/setup.bash
ros2 run rover_core rover_heartbeat_minimal
```

- Build, source, and run the heartbeat node.

```bash
ros2 node list
ros2 node info /rover_heartbeat_minimal
```

- Verify ROS 2 can see the running node.

## Tiny Terms

| Word | Quick meaning |
|---|---|
| Node | Running ROS 2 program |
| `rclpy` | Python library for ROS 2 nodes |
| Logger | ROS 2-style print |
| Spin | Keeps node processing work |
| Console script | Command used by `ros2 run` |
| `setup.py` | Registers Python commands |

## Remember

- Pattern: create file, register, build, source, run, verify.
- Package: `rover_core`; node: `rover_heartbeat_minimal`.
- If `ros2 run` cannot find it, check `setup.py`, rebuild, then source.
