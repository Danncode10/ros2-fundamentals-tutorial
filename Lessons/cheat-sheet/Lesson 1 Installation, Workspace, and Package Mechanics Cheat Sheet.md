# Lesson 1 Installation, Workspace, and Package Mechanics Cheat Sheet

## Big Picture

- `ros2_ws` is your ROS 2 learning workspace.
- Packages go inside `src/`; generated folders come from `colcon build`.
- Build, source, then verify that ROS 2 can see your package.

## Must Remember

- `source /opt/ros/jazzy/setup.bash` loads the system ROS 2 install.
- `source install/setup.bash` loads your local workspace after building.
- `colcon build` prepares workspace packages and creates `build/`, `install/`, and `log/`.
- `package.xml` marks a folder as a ROS 2 package.
- Python ROS 2 packages usually include `setup.py`.

## Key Words

| Word | Quick meaning |
|---|---|
| Workspace | Folder where ROS 2 packages are built together |
| `src/` | Source folder where package folders live |
| Package | Organized home for related ROS 2 code and future nodes |
| Node | A running ROS 2 program; learned properly in Phase 2 |
| `colcon` | Tool that builds ROS 2 workspaces |
| `build/` | Temporary build work |
| `install/` | Built package files ROS 2 can discover |
| `log/` | Build logs and error history |
| `package.xml` | ROS 2 package identity and dependency file |
| `setup.py` | Python package install and future run-command setup |
| Dependency | Something your package needs, such as `rclpy` |

## Tiny Diagram Or Mental Model

```text
ros2_ws/
├── src/
│   └── rover_core/
├── build/    generated
├── install/  generated
└── log/      generated
```

Mental model:

```text
src/ -> colcon build -> install/ -> source install/setup.bash -> ROS 2 can find package
```

## Commands To Recognize

```bash
echo $ROS_DISTRO
```

- Checks whether ROS 2 Jazzy is already sourced.

```bash
ros2 pkg list
```

- Lists packages visible to the current terminal.

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
```

- Creates and enters the workspace root.

```bash
colcon build
```

- Builds the workspace and creates `build/`, `install/`, and `log/`.

```bash
source install/setup.bash
```

- Sources the local workspace from the generated `install/` folder.

```bash
ros2 pkg create rover_core --build-type ament_python --dependencies rclpy
```

- Creates the first Python ROS 2 package.

```bash
ros2 pkg list | grep rover_core
ros2 pkg prefix rover_core
```

- Verifies that ROS 2 can see and locate `rover_core`.

## Quick Self-Check

- Can I explain why `ros2_ws` has a `src/` folder?
- Can I explain what `colcon build` creates?
- Can I explain why I source `install/setup.bash` after building?
- Can I tell the difference between a package and a node?
- Can I prove that ROS 2 can see `rover_core`?
