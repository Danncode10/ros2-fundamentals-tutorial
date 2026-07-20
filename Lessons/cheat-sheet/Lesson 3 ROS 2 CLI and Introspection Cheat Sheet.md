# Lesson 3 ROS 2 CLI and Introspection Cheat Sheet

## Big Picture

- **Introspection** means checking what ROS 2 can see while the system is running.
- Use CLI first for exact proof, then `rqt_graph` for a visual view.
- Runtime renaming changes a node name for one run only; it does not edit code or `setup.py`.

## Must Remember

- A node appears in `ros2 node list` only while it is alive.
- `ros2 node info /node_name` is an important debugging command.
- Empty subscribers, clients, and actions are normal for the beginner heartbeat node.
- `/rosout`, `/parameter_events`, and parameter services are built-in ROS 2 support.
- `rqt_graph` should be refreshed and fitted into view.
- `rqt_graph` is the shortcut; `rqt` is the plugin container.

## Key Words

| Word | Quick meaning |
|---|---|
| Introspection | Checking the live ROS 2 system |
| ROS graph | Runtime map of visible nodes and connections |
| Node name | Name ROS 2 sees while the node is running |
| Runtime renaming | Temporary name change when starting a node |
| Remapping | ROS 2 startup syntax for changing names |
| `rqt_graph` | GUI tool that shows the ROS graph |
| `rqt` | General GUI shell that loads plugins |

## Tiny Diagram Or Mental Model

```text
Terminal CLI                 GUI
ros2 node list       ->      rqt_graph
ros2 node info       ->      visual node graph
```

Runtime rename mental model:

```text
same executable + new runtime name = separate live node identity
```

## Commands To Recognize

```bash
source /opt/ros/jazzy/setup.bash
source ~/ros2_ws/install/setup.bash
```

- Sets up ROS 2 and the local workspace in the current terminal.

```bash
ros2 run rover_core rover_heartbeat_minimal
```

- Runs the original heartbeat node.

```bash
ros2 node list
```

- Shows which ROS 2 nodes are alive right now.

```bash
ros2 node info /rover_heartbeat_minimal
```

- Inspects one live node by name.

```bash
ros2 run rover_core rover_heartbeat_minimal --ros-args -r __node:=front_rover_heartbeat
```

- Runs the same executable with a temporary runtime node name.

```bash
ros2 run rover_core rover_heartbeat_minimal --ros-args -r __node:=test_rover_heartbeat
```

- Runs a second renamed copy in another terminal.

```bash
sudo apt install ros-jazzy-rqt ros-jazzy-rqt-graph
```

- Installs the lightweight GUI graph tools.

```bash
rqt_graph
```

- Opens the node graph directly. Click refresh, then fit graph in view.

```bash
rqt
```

- Opens the general GUI shell. Use `Plugins -> Introspection -> Node Graph`, then refresh.

## Quick Success Signs

- `ros2 node list` shows `/front_rover_heartbeat` and `/test_rover_heartbeat`.
- `ros2 node info /front_rover_heartbeat` prints node details.
- `ros2 node info /test_rover_heartbeat` prints node details.
- `rqt_graph` shows both node names after refresh.
- No line between the two nodes is normal because they are not using custom topics yet.

## Quick Self-Check

- Can I explain what introspection means?
- Can I prove a node is alive from the terminal?
- Can I explain why runtime renaming does not change the Python file?
- Can I run two copies of the same executable with different node names?
- Can I open `rqt_graph`, refresh it, and fit the graph in view?
