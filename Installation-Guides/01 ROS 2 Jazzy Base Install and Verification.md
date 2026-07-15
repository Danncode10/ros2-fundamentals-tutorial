# ROS 2 Jazzy Base Install and Verification

This guide installs and verifies the lightweight ROS 2 setup used at the beginning of this course.

Use this guide **before Lesson 1**. You will keep using this setup throughout the beginner course, especially when working with:

- ROS 2 commands
- workspaces
- packages
- Python nodes
- topics
- services
- custom interfaces
- parameters
- launch files
- command-line debugging

This guide does **not** install heavy robotics tools such as Gazebo, Navigation2, MoveIt, YOLO, Docker images, large simulation worlds, or the full ROS desktop stack. Those belong in a separate later guide.

---

# What This Setup Gives You

This setup installs:

- Ubuntu 24.04-compatible ROS 2 Jazzy base packages
- the `ros2` command
- the `colcon` build tool
- enough ROS 2 tools to start learning the fundamentals

This is the low-storage beginner setup.

It is enough for the early course modules:

| Course area | Is this setup enough? |
|---|---|
| Lesson 1 / environment setup | Yes |
| ROS 2 workspaces | Yes |
| Python packages | Yes |
| Nodes | Yes |
| Topics | Yes |
| Services | Yes |
| Custom interfaces | Yes |
| Parameters | Yes |
| Launch files | Yes |
| Basic CLI debugging | Yes |
| Gazebo / full simulation | No, later guide |
| Navigation2 / MoveIt / YOLO | No, later guide |

---

# Target System

This guide assumes:

- Ubuntu 24.04 LTS
- ROS 2 Jazzy
- a terminal
- limited storage is acceptable

Check your Ubuntu version:

```bash
lsb_release -a
```

Expected:

```text
Distributor ID: Ubuntu
Description:    Ubuntu 24.04.x LTS
Release:        24.04
Codename:       noble
```

If you see Ubuntu 24.04 and codename `noble`, you are on the correct Ubuntu version for ROS 2 Jazzy.

---

# Add the ROS 2 Package Repository

If Ubuntu says it cannot find `ros-jazzy-ros-base`, it usually means the ROS 2 repository has not been added yet.

Install required tools:

```bash
sudo apt update
sudo apt install software-properties-common curl gnupg lsb-release
sudo add-apt-repository universe
```

Add the ROS 2 signing key:

```bash
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key \
  -o /usr/share/keyrings/ros-archive-keyring.gpg
```

Add the ROS 2 apt repository:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

Update package lists:

```bash
sudo apt update
```

---

# Install ROS 2 Jazzy Base

Install the lightweight ROS 2 base setup:

```bash
sudo apt install ros-jazzy-ros-base
```

Install beginner development tools:

```bash
sudo apt install ros-dev-tools
```

`ros-jazzy-ros-base` gives you the core ROS 2 system.

`ros-dev-tools` gives you common development tools, including `colcon`, which builds ROS 2 workspaces.

---

# Source ROS 2

Before using ROS 2 in a terminal, run:

```bash
source /opt/ros/jazzy/setup.bash
```

This tells your terminal where ROS 2 is installed.

Check that the terminal knows the ROS 2 distribution:

```bash
echo $ROS_DISTRO
```

Expected:

```text
jazzy
```

Optional: make this automatic for new terminals:

```bash
echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

After this, new terminals should automatically know about ROS 2.

---

# Verify ROS 2 Commands

Check where the `ros2` command is:

```bash
which ros2
```

Expected:

```text
/opt/ros/jazzy/bin/ros2
```

Check where `colcon` is:

```bash
which colcon
```

Expected:

```text
/usr/bin/colcon
```

Check that ROS 2 help works:

```bash
ros2 --help
```

You should see a list of ROS 2 command groups such as:

```text
node
topic
service
param
pkg
launch
```

Check that ROS 2 can list installed packages:

```bash
ros2 pkg list
```

You should see many package names, such as:

```text
action_msgs
ament_cmake
builtin_interfaces
rclpy
std_msgs
```

If you only want to preview the first few packages, use:

```bash
ros2 pkg list | sed -n '1,20p'
```

Avoid using `ros2 pkg list | head` if it causes a `BrokenPipeError`. That error only means `head` stopped reading before `ros2` finished printing. It does not mean ROS 2 is broken.

---

# Verify Installed Packages

Check that ROS 2 base is installed:

```bash
dpkg -l | grep ros-jazzy-ros-base
```

Check that development tools are installed:

```bash
dpkg -l | grep ros-dev-tools
```

Check all installed ROS Jazzy packages:

```bash
dpkg -l | grep ros-jazzy
```

---

# Build a Test Workspace

This proves that `colcon` works and that your system can build a ROS 2 workspace.

Create an empty workspace:

```bash
mkdir -p ~/test_ws/src
cd ~/test_ws
```

Build it:

```bash
colcon build
```

Expected:

```text
Summary: 0 packages finished
```

This is okay. The workspace has no packages yet, so there is nothing to build. The important part is that `colcon build` finishes successfully.

Source the test workspace:

```bash
source install/setup.bash
echo "Workspace sourced successfully"
```

Expected:

```text
Workspace sourced successfully
```

---

# Lesson 1 Readiness Checklist

You are ready for Lesson 1 when all of these work:

```bash
source /opt/ros/jazzy/setup.bash
echo $ROS_DISTRO
which ros2
which colcon
ros2 --help
ros2 pkg list | sed -n '1,20p'
mkdir -p ~/test_ws/src
cd ~/test_ws
colcon build
source install/setup.bash
```

Success signs:

- `echo $ROS_DISTRO` prints `jazzy`
- `which ros2` points to `/opt/ros/jazzy/bin/ros2`
- `which colcon` points to `/usr/bin/colcon`
- `ros2 --help` prints ROS 2 command help
- `ros2 pkg list` prints package names
- `colcon build` finishes successfully
- `source install/setup.bash` does not show an error

If all of these pass, your lightweight ROS 2 beginner setup is ready.

---

# Common Problems

| Problem | Likely cause | Fix |
|---|---|---|
| `E: Unable to locate package ros-jazzy-ros-base` | ROS 2 apt repository is missing | Add the ROS 2 repository, then run `sudo apt update` |
| `/opt/ros/jazzy/setup.bash: No such file or directory` | ROS 2 Jazzy is not installed yet | Install `ros-jazzy-ros-base` |
| `ros2: command not found` | ROS 2 is installed, but this terminal has not loaded it yet | Temporary fix: run `source /opt/ros/jazzy/setup.bash`. Permanent fix for new terminals: run `echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc` then `source ~/.bashrc` |
| `colcon: command not found` | Development tools are missing | Run `sudo apt install ros-dev-tools` |
| `Summary: 0 packages finished` | Empty workspace | This is normal for a test workspace |
| `BrokenPipeError` after using `head` | `head` closed the output early | Use `sed -n '1,20p'` instead |

---

# What Comes Later

Do not install heavy robotics tools yet unless a later guide asks for them.

Later installation guides can cover:

- `rqt` and `rqt_graph`
- RViz
- Gazebo / Ignition
- Navigation2
- MoveIt
- camera and perception tools
- YOLO or AI packages
- larger simulation environments

For now, this lightweight setup is enough to begin learning ROS 2 properly.
