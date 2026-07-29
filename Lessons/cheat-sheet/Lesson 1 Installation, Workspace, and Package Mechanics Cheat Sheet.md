# Lesson 1 Installation, Workspace, and Package Mechanics Cheat Sheet

## Lesson Reminder

Create `~/ros2_ws`, create the `rover_core` Python package, build it, source it, and prove ROS 2 can see it.

## Commands

```bash
echo $ROS_DISTRO
source /opt/ros/jazzy/setup.bash
ros2 --help
```

- Check ROS 2 Jazzy and load it if needed.

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
colcon build
source install/setup.bash
```

- Create, build, and source the empty workspace.

```bash
cd ~/ros2_ws/src
ros2 pkg create rover_core --build-type ament_python --dependencies rclpy
```

- Create the first Python package.

```bash
cd ~/ros2_ws
colcon build
source install/setup.bash
```

- Rebuild after adding `rover_core`, then source again.

```bash
ros2 pkg list | grep rover_core
ros2 pkg prefix rover_core
ls ~/ros2_ws
ls ~/ros2_ws/src/rover_core
```

- Verify the package is visible and the workspace folders exist.

## Tiny Terms

| Word | Quick meaning |
|---|---|
| Workspace | Folder where ROS 2 packages are built |
| `src/` | Source packages go here |
| Package | Container for related ROS 2 code |
| `colcon` | Build tool |
| Source | Load setup into this terminal |
| `package.xml` | Package metadata |
| `setup.py` | Python package setup |

## Remember

- Build from `~/ros2_ws`, not from `~/ros2_ws/src`.
- Source after every build: `source install/setup.bash`.
- Do not edit `build/`, `install/`, or `log/`.
