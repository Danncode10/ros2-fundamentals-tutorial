# Lesson 1 Installation, Workspace, and Package Mechanics Cheat Sheet

## Main Idea

Create `~/ros2_ws`, create `rover_core`, build it, source it, and prove ROS 2 can find it.

## Setup Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `echo $ROS_DISTRO` | Print the ROS 2 distribution this terminal sees. | Checking if ROS 2 is already loaded. | It prints `jazzy`. |
| `source /opt/ros/jazzy/setup.bash` | Load the system ROS 2 Jazzy environment into this terminal. | `echo $ROS_DISTRO` is blank or `ros2` is missing. | No error; usually no output. |
| `ros2 --help` | Ask the `ros2` command to show help. | Checking that ROS 2 commands work. | Help text appears. |

## Workspace Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `mkdir -p ~/ros2_ws/src` | Create the workspace folder and its `src` folder. | Starting the ROS 2 workspace. | Folder exists. |
| `cd ~/ros2_ws` | Move into the workspace root. | Before building. | `pwd` ends in `ros2_ws`. |
| `colcon build` | Build the packages in the workspace. | After creating or changing packages. | Build finishes without errors. |
| `source install/setup.bash` | Load your built workspace into this terminal. | After every successful build. | No error; usually no output. |

## Package Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `cd ~/ros2_ws/src` | Move to where source packages belong. | Before creating `rover_core`. | You are inside `src`. |
| `ros2 pkg create rover_core --build-type ament_python --dependencies rclpy` | Create a Python ROS 2 package named `rover_core` that depends on `rclpy`. | Creating the first package. | `rover_core` folder appears. |
| `ros2 pkg list \| grep rover_core` | Search visible ROS 2 packages for `rover_core`. | Verifying build + source worked. | It prints `rover_core`. |
| `ros2 pkg prefix rover_core` | Show where ROS 2 found the built package. | Checking the package location. | Path points inside `~/ros2_ws/install/rover_core`. |

## Tiny Terms

| Term | Meaning |
|---|---|
| Workspace | Folder where ROS 2 packages are built together. |
| `src/` | Folder where package source code goes. |
| Package | Container for ROS 2 code and metadata. |
| `colcon` | Tool that builds ROS 2 workspaces. |
| Source | Load setup information into the current terminal. |
| `package.xml` | Package metadata and dependencies. |
| `setup.py` | Python package setup file. |

## Remember

- Build from `~/ros2_ws`, not from `~/ros2_ws/src`.
- After building, always run `source install/setup.bash`.
- Do not edit generated `build/`, `install/`, or `log/` folders.
