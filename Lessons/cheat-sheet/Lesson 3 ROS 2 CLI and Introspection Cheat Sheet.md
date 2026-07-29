# Lesson 3 ROS 2 CLI and Introspection Cheat Sheet

## Main Idea

Use CLI and `rqt_graph` to inspect what ROS 2 can see while nodes are running.

## Node Inspection Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `source /opt/ros/jazzy/setup.bash` | Load system ROS 2 into this terminal. | Opening a new terminal. | No error. |
| `source ~/ros2_ws/install/setup.bash` | Load your workspace package commands. | Before running `rover_core` nodes. | No error. |
| `ros2 run rover_core rover_heartbeat_minimal` | Start the heartbeat node. | Creating something live to inspect. | Heartbeat logs repeat. |
| `ros2 node list` | List live ROS 2 node names. | Checking what is running. | Node names appear. |
| `ros2 node info /rover_heartbeat_minimal` | Show details about one live node. | Inspecting exact runtime details. | Node info prints. |

## Runtime Rename Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `ros2 run rover_core rover_heartbeat_minimal --ros-args -r __node:=front_rover_heartbeat <you_can_add_more_arguments>` | Run the same executable with a temporary node name. | Testing a renamed copy. | `/front_rover_heartbeat` appears. |
| `ros2 run rover_core rover_heartbeat_minimal --ros-args -r __node:=test_rover_heartbeat` | Run a second renamed copy in another terminal. | Testing two live copies. | `/test_rover_heartbeat` appears. |
| `ros2 node info /front_rover_heartbeat` | Inspect the renamed front node. | Checking the renamed copy. | Node info prints. |
| `ros2 node info /test_rover_heartbeat` | Inspect the renamed test node. | Checking the second copy. | Node info prints. |

## Graph Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `sudo apt update` | Refresh Ubuntu package lists. | Before installing tools. | Finishes without errors. |
| `sudo apt install ros-jazzy-rqt ros-jazzy-rqt-graph` | Install lightweight ROS 2 graph tools. | Before using `rqt_graph`. | Install completes. |
| `rqt_graph` | Open the ROS graph viewer directly. | Visualizing live nodes. | Window shows nodes after refresh. |
| `rqt` | Open the general ROS GUI plugin app. | Opening Node Graph from plugins. | `rqt` window opens. |

## Tiny Terms

| Term | Meaning |
|---|---|
| Introspection | Inspecting the live ROS 2 system. |
| ROS graph | Runtime map of visible nodes and connections. |
| Node name | Name ROS 2 sees while the node runs. |
| Remapping | Changing a name at runtime. |
| `rqt_graph` | Direct visual graph tool. |

## Remember

- A node appears only while the program is running.
- Runtime renaming does not edit the Python file or `setup.py`.
- Use `ros2 node list` first, then copy the exact name into `ros2 node info`.
