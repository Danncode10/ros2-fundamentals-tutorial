# Lesson 3 ROS 2 CLI and Introspection Cheat Sheet

## Lesson Reminder

Use CLI and `rqt_graph` to inspect live ROS 2 nodes instead of guessing.

## Commands

```bash
source /opt/ros/jazzy/setup.bash
source ~/ros2_ws/install/setup.bash
ros2 run rover_core rover_heartbeat_minimal
```

- Run the original heartbeat node.

```bash
ros2 node list
ros2 node info /rover_heartbeat_minimal
```

- List live nodes and inspect one node by exact name.

```bash
ros2 run rover_core rover_heartbeat_minimal --ros-args -r __node:=front_rover_heartbeat
```

- Run the same executable with a temporary node name.

```bash
ros2 run rover_core rover_heartbeat_minimal --ros-args -r __node:=test_rover_heartbeat
```

- Run a second renamed copy in another terminal.

```bash
ros2 node list
ros2 node info /front_rover_heartbeat
ros2 node info /test_rover_heartbeat
```

- Prove both renamed nodes are alive.

```bash
sudo apt update
sudo apt install ros-jazzy-rqt ros-jazzy-rqt-graph
rqt_graph
rqt
```

- Install and open the lightweight graph tools.

## Tiny Terms

| Word | Quick meaning |
|---|---|
| Introspection | Inspect the live ROS 2 system |
| ROS graph | Runtime map of visible nodes/connections |
| Node name | Name ROS 2 sees while node runs |
| Remapping | Runtime name change |
| `rqt_graph` | Direct graph viewer |
| `rqt` | GUI plugin container |

## Remember

- A node appears only while the program is running.
- Runtime renaming does not edit Python code or `setup.py`.
- Use `ros2 node list` first, then copy the exact name into `ros2 node info`.
