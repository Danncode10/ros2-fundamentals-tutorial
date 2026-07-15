# ROS 2-Only Learning Roadmap

## Course Goal

By the end of this ROS 2 curriculum, you should be able to build and understand a complete simulated ROS 2 software stack for your agricultural rover:

- Rover system nodes
- Sensor publishers
- Motor command subscribers
- Diagnostic services
- Custom messages
- Parameters
- Launch files
- CLI debugging
- rqt/rqt_graph visualization
- A final mini rover software project

This course will **not** focus on YOLO, Supabase, dashboards, cloud systems, or frontend work. Those belong later. This is strictly ROS 2 fundamentals.

---

# How to Use This Roadmap

This file is the **lesson plan**, not the finished course content.

Use it as the structure for building the course while learning ROS 2 yourself. Each phase defines what must be learned, practiced, verified, and connected back to the rover project. The detailed lessons should be written one section at a time as you study, test commands, write code, and discover common mistakes.

Good workflow:

1. Study one section.
2. Write the actual lesson for that section.
3. Test every command in a clean terminal.
4. Build the smallest working rover example.
5. Add troubleshooting notes while the mistakes are fresh.
6. Add a checkpoint so the learner knows whether they are ready to continue.

Do not rush to write all lessons before testing them. ROS 2 learning is very environment-sensitive, so the course should grow from real terminal practice.

---

# Learner Assumptions

This course assumes the learner:

- Is comfortable using a terminal at a beginner level.
- Can create folders and edit text files.
- Knows basic Python syntax:
  - variables
  - functions
  - imports
  - simple classes
  - running Python files
- Understands basic robotics ideas at a high level:
  - sensors produce data
  - motors receive commands
  - a robot needs control logic
  - debugging matters

This course does **not** assume prior ROS 2 experience.

If the learner is weak in Python, add short Python refreshers before Phase 2. Do not let Python confusion disguise itself as ROS 2 confusion.

---

# Course Development Rule

Because this course is being built while learning the field, every lesson should separate three things:

1. **What ROS 2 concept is being learned**
2. **What rover behavior it supports**
3. **How the learner proves it works**

Avoid writing lessons that only explain concepts. Every concept should end with a small working artifact, a terminal check, and a clear pass/fail condition.

---

# Installation Strategy

This course uses a **progressive installation approach**.

The goal is to learn ROS 2 fundamentals first without filling the computer with heavy robotics tools too early.

Recommended setup:

- Ubuntu 24.04 LTS
- ROS 2 Jazzy
- Start with the lightweight ROS 2 base installation
- Add small GUI debugging tools only when the lesson actually needs them
- Add simulation tools much later, only if a later course or project requires them

Why:

- Early lessons focus on concepts, terminals, Python nodes, workspaces, topics, services, parameters, and launch files.
- These do not need Gazebo, full simulation stacks, Navigation2, MoveIt, Docker, YOLO, or large AI packages.
- A smaller setup is easier to understand, easier to fix, and safer for limited storage.

Install timing:

| Course point | Install level | Purpose |
|---|---|---|
| Phase 1 | ROS 2 Jazzy base | Core ROS 2 commands, Python nodes, workspaces, packages |
| Phase 3 | rqt and rqt_graph only | Visual graph debugging |
| Later course, after fundamentals | Heavy tools only if needed | Simulation, navigation, manipulation, perception |

Avoid installing these during the beginner course unless a future lesson specifically requires them:

- Full ROS desktop stack
- Gazebo / Ignition simulation
- Navigation2
- MoveIt
- Docker images
- YOLO / AI vision dependencies
- Large rover simulation worlds

For a low-storage VM, this course should begin with:

```bash
ros-jazzy-ros-base
```

Then add only the small visualization tools when Module 3 starts:

```bash
ros-jazzy-rqt
ros-jazzy-rqt-graph
```

---

# Low-Storage Learning Path

This course is designed to be friendly to a small-storage computer, including a MacBook Air M1 running Ubuntu in a VM or similar constrained setup.

The beginner path should stay lightweight:

- Use `ros-jazzy-ros-base` first.
- Use terminal-based ROS 2 commands heavily.
- Write small Python nodes.
- Build small workspaces and packages.
- Use CLI debugging before graphical tools.
- Add only `rqt` and `rqt_graph` when the graph becomes useful to see visually.

The beginner modules should work without:

- Gazebo / Ignition simulation
- Navigation2
- MoveIt
- Docker images
- YOLO or AI vision packages
- large simulation worlds
- large datasets
- full desktop robotics stacks

This is not a weakness in the course. It is the intended learning path. ROS 2 fundamentals can be learned very well without heavy graphics or simulation tools.

Storage-friendly learning order:

| Stage | Tools | Why |
|---|---|---|
| Early beginner | `ros-jazzy-ros-base`, terminal, Python editor | Learn the ROS 2 communication model clearly |
| Middle beginner | `rqt`, `rqt_graph` | Visualize nodes and topics without installing full simulation |
| After fundamentals | optional SSD or larger storage | Prepare for Gazebo, RViz, Nav2, robot models, perception, and larger projects |

Move to heavier tools only when at least one of these is true:

- You can already create and run ROS 2 Python nodes.
- You understand topics, services, parameters, and launch files.
- You can debug a small ROS 2 graph from the CLI.
- You need simulation, visualization, navigation, manipulation, or perception for the next real project.
- You have enough disk space, such as an external SSD, to install and maintain the larger tools safely.

If storage is tight, do not install `ros-jazzy-desktop` at the start. Begin small, learn the core ideas deeply, and expand later.

---

# Mac Host and Ubuntu VM Workflow

The course author may write lessons and course files on macOS using Codex or Claude, while running ROS 2 inside an Ubuntu VM.

A shared folder, such as a Spice client folder, is useful for quick file transfer, screenshots, and reading course notes from both systems. Do not treat the shared folder as the main place to build ROS 2 workspaces.

Recommended code workflow:

1. Edit lesson files or source examples on macOS using Codex or Claude.
2. Save the work through Git by committing, stashing, or pushing to a remote repository.
3. In Ubuntu, use Git to pull, fetch, or switch to the same work.
4. Run ROS 2 commands and tests inside Ubuntu.

This keeps macOS as the comfortable authoring environment and Ubuntu as the clean ROS 2 testing environment.

Companion ROS 2 workspace repo:

```text
https://github.com/Danncode10/ros2_ws
```

For beginner ROS 2 practice, keep the actual ROS 2 workspace simple:

```bash
~/ros2_ws
```

Why:

- ROS 2 commands are run inside Ubuntu.
- `colcon build` generates `build/`, `install/`, and `log/` folders.
- VM shared folders can sometimes have slower file access, permission differences, or symlink behavior that confuses beginner troubleshooting.
- Shared folder paths often contain spaces, which makes terminal commands harder for beginners.
- Git gives a clearer history of what changed and makes it easier to move tested work between macOS and Ubuntu.

Install Git in Ubuntu if needed:

```bash
sudo apt update
sudo apt install git
```

Recommended workflow:

| Work | Best place |
|---|---|
| Edit course Markdown with Codex or Claude | macOS project folder |
| Save or move work between machines | Git commit, stash, push, pull, or fetch |
| Quick screenshots or one-off file transfer | Spice or VM shared folder |
| Run ROS 2 commands | Ubuntu terminal |
| Build beginner ROS 2 workspaces | `~/ros2_ws` inside Ubuntu |
| Save polished course examples | Commit them back into the course repository when ready |

This keeps the course easy to edit while keeping ROS 2 practice clean, repeatable, and predictable.

---

# Phase 0: Orientation

## Section 0.1: What ROS 2 Is

**Purpose:** Understand why ROS 2 exists before writing commands.

Topics:

- What ROS 2 does
- Why robotics software is split into nodes
- Why robots need message passing
- Why ROS 2 is useful for your rover
- Difference between normal Python scripts and ROS 2 programs
- What “distributed robotics software” means

Rover analogy:

- The rover is not one big program.
- It is a team of small programs:
  - IMU node
  - motor node
  - arm controller node
  - diagnostics node
  - navigation node
  - vision node later

Mini activity:

- Draw the future rover software graph on paper:
  - Sensors publish data
  - Controllers subscribe to data
  - Diagnostics answer requests
  - Parameters tune behavior
  - Launch files start everything

No coding yet.

---

# Phase 1: Installation, Workspace, and Package Mechanics

## Section 1.1: ROS 2 Distribution and Environment

Recommended target:

- ROS 2 Jazzy
- Ubuntu 24.04

Topics:

- What a ROS 2 distribution is
- Why Jazzy is appropriate
- What `source /opt/ros/jazzy/setup.bash` does
- Why terminal environment matters
- What happens when ROS 2 is “not sourced”

Practice:

- Read and complete the existing installation guide:
  - `Installation-Guides/01 ROS 2 Jazzy Base Install and Verification.md`
- Check ROS 2 installation
- Run a built-in ROS 2 demo
- Understand environment variables at a beginner level

Installation rule:

- Do not install the full ROS desktop stack yet.
- Do not install Gazebo yet.
- Use the smallest ROS 2 setup that lets you learn the core system clearly.

Expected skill:

- You can open a terminal and verify that ROS 2 commands exist.

---

## Section 1.2: Create Your First Workspace

Workspace name:

```bash
ros2_ws
```

This name is intentionally general. The learner is here to master ROS 2 first, not to start thesis-specific work too early.

Topics:

- What a ROS 2 workspace is
- Why source code goes inside `src/`
- What `colcon build` does
- What `install/`, `build/`, and `log/` folders mean
- Difference between system ROS packages and your own packages

Rover connection:

- `ros2_ws` becomes the learning workspace for ROS 2 fundamentals.
- Later, after the fundamentals are comfortable, the same workspace skills will be used to build the agricultural rover software stack.

Practice:

- Create workspace folder
- Create `src/`
- Build empty workspace
- Source local workspace

Expected skill:

- You understand the physical folder layout of a ROS 2 project.

---

## Section 1.3: Create a Python Package

Package name:

```bash
rover_core
```

Topics:

- What a ROS 2 package is
- Why packages exist
- Python package structure
- `package.xml`
- `setup.py`
- Console scripts
- Package dependencies

Rover connection:

- `rover_core` will hold your first rover nodes:
  - heartbeat node
  - fake IMU node
  - motor monitor node
  - diagnostics node

Practice:

- Create a Python ROS 2 package
- Build it
- Source it
- Confirm ROS 2 can see it

Expected skill:

- You can create a ROS 2 Python package without panic.

---

# Phase 2: Nodes

## Section 2.1: What a Node Is

Topics:

- Node definition
- Why one robot uses many nodes
- Node names
- Node lifecycle at a beginner level
- Difference between a normal Python script and a ROS 2 node

Rover connection:

Example rover nodes:

- `rover_heartbeat`
- `imu_sensor_sim`
- `motor_controller`
- `arm_stabilizer`
- `diagnostics_server`

Mini-project:

- Create a node that prints:

```text
Rover core system is awake
```

No topics yet. No services yet. Just a node.

---

## Section 2.2: Python Node, Minimal Code First

Topics:

- `rclpy.init()`
- Creating a node
- Logging
- Spinning
- Shutting down

Style:

- Very basic procedural Python first
- No classes yet

Rover mini-project:

- `rover_heartbeat_minimal`
- Prints a heartbeat message every second

Expected skill:

- You understand the smallest possible Python ROS 2 node.

---

## Section 2.3: Python Node with OOP

Topics:

- Why ROS 2 nodes are often written as classes
- `class RoverHeartbeat(Node)`
- Constructor
- Timers
- Logger

Rover mini-project:

- Refactor heartbeat node into OOP

Expected skill:

- You can recognize and write the common ROS 2 Python node pattern.

---

# Phase 3: ROS 2 CLI and Introspection

## Section 3.1: Inspect Running Nodes

Topics:

- `ros2 node list`
- `ros2 node info`
- Node names
- Runtime visibility

Rover practice:

- Run `rover_heartbeat`
- Check if ROS 2 can see it
- Inspect the node

Expected skill:

- You can confirm whether your node is actually alive.

---

## Section 3.2: Rename Nodes at Runtime

Topics:

- Why runtime renaming is useful
- Avoiding node name conflicts
- Basic remapping syntax

Rover example:

- Run two heartbeat nodes:
  - `front_rover_heartbeat`
  - `test_rover_heartbeat`

Expected skill:

- You understand that node names are part of the ROS graph.

---

## Section 3.3: rqt and rqt_graph

Topics:

- What visual introspection means
- rqt basics
- rqt_graph basics
- Why visual tools help robotics debugging

Install now, not earlier:

- `rqt`
- `rqt_graph`

Rover practice:

- Run heartbeat node
- Open rqt_graph
- See the graph even before topics become complex

Expected skill:

- You can visually inspect the ROS graph.

---

# Phase 4: Topics

## Section 4.1: What a Topic Is

Topics:

- Publisher
- Subscriber
- Message
- Topic name
- One-to-many communication
- Continuous data streams

Rover connection:

Topics are perfect for repeated sensor data:

- IMU pitch/roll
- wheel encoder ticks
- motor speed commands
- arm target pose
- rover velocity

---

## Section 4.2: Minimal Python Publisher

Rover mini-project:

```text
imu_sensor_sim
```

Publishes fake chassis tilt:

```text
pitch: 5.0
roll: -2.0
```

Start simple with `std_msgs/String`.

Topics:

- Creating a publisher
- Timer callbacks
- Publishing messages
- Topic names

Expected skill:

- You can stream fake sensor data.

---

## Section 4.3: Minimal Python Subscriber

Rover mini-project:

```text
tilt_monitor
```

Subscribes to fake IMU tilt messages.

Topics:

- Creating a subscriber
- Callback functions
- Reading incoming messages
- Logging received data

Expected skill:

- You can receive sensor data from another node.

---

## Section 4.4: Publisher and Subscriber Together

Mini system:

```text
imu_sensor_sim  --->  tilt_monitor
```

Practice:

- Run both nodes
- Inspect with CLI
- Inspect with rqt_graph
- Echo topic data

Commands introduced:

```bash
ros2 topic list
ros2 topic echo
ros2 topic info
ros2 topic hz
```

Expected skill:

- You understand live ROS 2 data flow.

---

## Section 4.5: Rover Motor Reaction

Rover mini-project:

```text
imu_sensor_sim  --->  motor_safety_monitor
```

Behavior:

- If pitch is safe, log normal operation
- If pitch is too high, log warning
- If roll is too high, log warning

Still simple. No real motor control yet.

Expected skill:

- You begin connecting sensor data to robot decision logic.

---

## Section 4.6: Topic Remapping

Topics:

- Why remapping exists
- Reusing nodes with different topic names

Rover example:

- Same IMU simulator publishes to:
  - `/front_imu`
  - `/rear_imu`
  - `/test_imu`

Expected skill:

- You can reuse nodes without editing code.

---

## Section 4.7: ROS 2 Bags

Topics:

- Why recording robot data matters
- Record topic data
- Replay topic data

Rover connection:

- Record fake IMU tilt data
- Replay it into the motor safety node

Expected skill:

- You understand the beginner version of robotics data logging.

---

# Phase 5: Services

## Section 5.1: What a Service Is

Topics:

- Request/response communication
- Difference between topics and services
- When not to use services
- Service server
- Service client

Rover connection:

Services are good for one-time questions:

- “Run battery diagnostic”
- “Check motor status”
- “Calibrate IMU”
- “Reset rover state”

---

## Section 5.2: Python Service Server

Rover mini-project:

```text
diagnostics_server
```

Service behavior:

Request:

```text
Run diagnostics?
```

Response:

```text
Battery OK, motors OK, IMU OK
```

Start with built-in service types first.

Expected skill:

- You can create a node that answers requests.

---

## Section 5.3: Python Service Client, No OOP

Rover mini-project:

```text
diagnostics_client_minimal
```

Topics:

- Waiting for a service
- Sending a request
- Reading a response

Expected skill:

- You can manually request rover diagnostics.

---

## Section 5.4: Python Service Client with OOP

Rover mini-project:

```text
diagnostics_client
```

Topics:

- Cleaner class-based client
- Reusable service calling structure

Expected skill:

- You can build a reusable diagnostic request tool.

---

## Section 5.5: Service Introspection

Commands:

```bash
ros2 service list
ros2 service type
ros2 service call
```

Rover practice:

- Call diagnostics from the command line
- Call diagnostics from your client node

Expected skill:

- You can test services without always writing client code.

---

# Phase 6: Custom Interfaces

## Section 6.1: What Interfaces Are

Topics:

- Messages
- Services
- Actions, only conceptually for now
- Why built-in message types are not always enough

Rover connection:

Your rover needs custom data shapes:

- IMU tilt data
- wheel encoder data
- tomato detection data
- arm compensation command
- rover diagnostic result

---

## Section 6.2: Create a Custom Message Package

Package name:

```bash
rover_interfaces
```

Topics:

- Why custom interfaces often live in their own package
- `.msg` files
- Building interfaces
- Sourcing after build

Expected skill:

- You understand where custom ROS 2 data types live.

---

## Section 6.3: Custom IMU Tilt Message

Message:

```text
float32 pitch
float32 roll
float32 yaw
```

Possible name:

```text
Tilt.msg
```

Rover mini-project:

- Replace fake `String` IMU data with structured `Tilt.msg`

System:

```text
imu_sensor_sim  --->  tilt_monitor
```

Expected skill:

- You can use proper structured rover sensor messages.

---

## Section 6.4: Custom Motor Command Message

Message:

```text
float32 left_speed
float32 right_speed
bool safety_limited
```

Possible name:

```text
MotorCommand.msg
```

Rover mini-project:

```text
imu_sensor_sim  --->  motor_safety_node  --->  motor_command_monitor
```

Expected skill:

- You can chain multiple ROS 2 nodes using custom messages.

---

## Section 6.5: Custom Tomato Detection Message

Even though YOLO itself is not part of this ROS 2 basics course, we can define the message early.

Message:

```text
string label
float32 confidence
int32 x
int32 y
int32 width
int32 height
```

Possible name:

```text
TomatoDetection.msg
```

Rover mini-project:

- Fake vision node publishes tomato detections
- Detection monitor prints result

Expected skill:

- You prepare ROS 2 interfaces for future vision work without doing AI yet.

---

## Section 6.6: Custom Service

Possible service:

```text
RunDiagnostics.srv
```

Request:

```text
bool check_battery
bool check_motors
bool check_imu
```

Response:

```text
bool success
string report
```

Rover mini-project:

- Replace generic diagnostics service with custom rover diagnostic service

Expected skill:

- You can design request/response interfaces for your robot.

---

# Phase 7: Parameters

## Section 7.1: What Parameters Are

Topics:

- Runtime configuration
- Why values should not always be hardcoded
- Parameter server concept
- Declaring parameters
- Getting parameters

Rover connection:

Good rover parameters:

- max speed
- safe pitch limit
- safe roll limit
- heartbeat interval
- diagnostics mode
- simulated battery level

---

## Section 7.2: Use Parameters in Python Nodes

Rover mini-project:

```text
motor_safety_node
```

Parameters:

```text
max_pitch_deg
max_roll_deg
max_motor_speed
```

Behavior:

- If tilt exceeds parameter limit, reduce speed
- If within limit, allow normal speed

Expected skill:

- You can tune rover behavior without rewriting logic.

---

## Section 7.3: Change Parameters from CLI

Commands:

```bash
ros2 param list
ros2 param get
ros2 param set
ros2 param describe
```

Rover practice:

- Change max pitch limit while node is running
- Observe behavior difference

Expected skill:

- You can tune a live node from the terminal.

---

## Section 7.4: YAML Parameter Files

Topics:

- Why parameter files exist
- YAML structure
- Loading parameter files

Rover config example:

```yaml
motor_safety_node:
  ros__parameters:
    max_pitch_deg: 12.0
    max_roll_deg: 10.0
    max_motor_speed: 0.6
```

Expected skill:

- You can store rover tuning values cleanly.

---

## Section 7.5: Parameter Callbacks

Topics:

- Reacting when parameters change
- Rejecting invalid values
- Protecting robot behavior

Rover example:

- Reject negative max speed
- Reject unsafe tilt thresholds

Expected skill:

- You understand beginner-level runtime safety tuning.

---

# Phase 8: Launch Files

## Section 8.1: What Launch Files Are

Topics:

- Why starting nodes manually becomes painful
- Launch files as robot startup scripts
- XML launch files
- Python launch files

Rover connection:

Instead of opening many terminals:

```text
Start rover core system with one command.
```

---

## Section 8.2: Create a Basic Launch File

Package:

```text
rover_core
```

Launch file:

```text
rover_bringup.launch.py
```

Starts:

- `rover_heartbeat`
- `imu_sensor_sim`
- `tilt_monitor`

Expected skill:

- You can boot a small ROS 2 system with one command.

---

## Section 8.3: Launch with Parameters

Launch starts:

- `motor_safety_node`

And loads:

```text
rover_safety.yaml
```

Expected skill:

- You can start nodes with config files.

---

## Section 8.4: Launch with Remapping

Rover example:

- Remap `/tilt` to `/simulated_imu/tilt`
- Remap motor command output for testing

Expected skill:

- You understand how launch files reshape the graph.

---

## Section 8.5: Namespaces

Topics:

- What namespaces are
- Why robots use them
- Avoiding topic collisions

Rover example:

```text
/rover1/imu/tilt
/rover1/motor/cmd
```

Future use:

- Multiple rover simulation
- Testing duplicate subsystems

Expected skill:

- You can organize larger ROS 2 systems.

---

# Phase 9: Beginner Rover Integration Project

## Final Project: Simulated Rover Core

This replaces the Udemy Turtlesim-style final project.

You will build a small but complete ROS 2 rover system.

Nodes:

```text
rover_heartbeat
imu_sensor_sim
motor_safety_node
motor_command_monitor
diagnostics_server
diagnostics_client
fake_tomato_detector
tomato_detection_monitor
```

Custom messages:

```text
Tilt.msg
MotorCommand.msg
TomatoDetection.msg
```

Custom service:

```text
RunDiagnostics.srv
```

Parameters:

```text
max_pitch_deg
max_roll_deg
max_motor_speed
heartbeat_interval
```

Launch file:

```text
rover_core.launch.py
```

Visual tools:

- `ros2 node list`
- `ros2 topic list`
- `ros2 topic echo`
- `ros2 service list`
- `ros2 param list`
- `rqt_graph`

Expected final graph:

```text
imu_sensor_sim
   |
   v
motor_safety_node
   |
   v
motor_command_monitor

fake_tomato_detector
   |
   v
tomato_detection_monitor

diagnostics_client
   |
   v
diagnostics_server

rover_heartbeat
```

By the end, you should be able to explain:

- What each node does
- What each topic carries
- What each service answers
- What each parameter controls
- How launch files start the system
- How to debug the graph using CLI and rqt

---

# Suggested Lesson Order

## Module 1: ROS 2 Environment and Workspace

Outcome:

- You complete the existing lightweight ROS 2 base installation guide
- You can create `ros2_ws`
- You can create `rover_core`
- You can build and source your workspace

No custom robot logic yet.

---

## Module 2: First Rover Node

Outcome:

- You understand ROS 2 nodes
- You create `rover_heartbeat`
- You write minimal Python first, then OOP

---

## Module 3: CLI and Visual Debugging

Outcome:

- You add only the small rqt tools needed for graph visualization
- You inspect nodes
- You use `ros2 node`
- You use `rqt_graph`

---

## Module 4: Topics

Outcome:

- You publish fake IMU data
- You subscribe to fake IMU data
- You inspect topics
- You record and replay topic data

---

## Module 5: Services

Outcome:

- You create a rover diagnostics server
- You create a diagnostics client
- You call services from the CLI

---

## Module 6: Custom Interfaces

Outcome:

- You create `rover_interfaces`
- You define rover-specific messages
- You use custom messages in Python nodes
- You define a custom diagnostic service

---

## Module 7: Parameters

Outcome:

- You tune rover safety limits
- You use YAML config files
- You change parameters live

---

## Module 8: Launch Files

Outcome:

- You start the rover system with one command
- You load parameters
- You apply remappings
- You use namespaces

---

## Module 9: Final Beginner Project

Outcome:

- You combine everything into one simulated rover core system
- You can explain and debug the full ROS 2 graph

---

# Required Deliverables by Module

Each module should produce something visible, runnable, or explainable. This prevents passive learning.

| Module | Required deliverable |
|---|---|
| Module 1 | Working ROS 2 environment, `ros2_ws`, `src/`, successful empty `colcon build` |
| Module 2 | Runnable `rover_heartbeat` node in minimal and OOP versions |
| Module 3 | Screenshots or notes proving `ros2 node` and `rqt_graph` were used |
| Module 4 | Working publisher/subscriber pair, topic echo output, recorded and replayed bag |
| Module 5 | Working diagnostics service server and client, plus CLI service call |
| Module 6 | `rover_interfaces` package with custom messages and custom service |
| Module 7 | Parameterized safety node with live CLI tuning and YAML config |
| Module 8 | Launch file that starts multiple rover nodes with parameters and remaps |
| Module 9 | Final rover core system, final graph, explanation of every node/topic/service/parameter |

Each deliverable should be small enough to finish, but complete enough to prove the learner actually understands the concept.

---

# Checkpoints and Assessments

Add a checkpoint at the end of every module.

Each checkpoint should include:

- **Concept check:** Can the learner explain the idea in plain words?
- **Command check:** Can the learner run the correct ROS 2 CLI commands?
- **Code check:** Can the learner point to the file that implements the behavior?
- **Debug check:** Can the learner inspect whether the system is alive?
- **Rover check:** Can the learner explain how this helps the agricultural rover?

Use short questions, not long exams.

Example checkpoint questions:

- What is the difference between a node and a topic?
- Why does a ROS 2 terminal need to be sourced?
- How do you prove that a node is running?
- When should rover data use a topic instead of a service?
- Why should IMU tilt use a custom message instead of a plain string?
- What parameter would you change to make the rover more conservative on slopes?

Passing a module means the learner can run the code, inspect it, and explain it without simply copying commands.

---

# Troubleshooting Notes to Add While Building Lessons

Every lesson should collect beginner mistakes as they happen.

Important troubleshooting categories:

- ROS 2 command not found
- Forgot to source `/opt/ros/jazzy/setup.bash`
- Forgot to source `install/setup.bash`
- Package not found
- Executable not found
- `colcon build` fails
- Python import error
- Custom message not generated
- Service call format is wrong
- Topic exists but no data is flowing
- rqt_graph is empty or missing expected nodes
- Parameter set command fails
- Launch file starts but one node silently fails

Each troubleshooting entry should include:

1. Symptom
2. Likely cause
3. Command to inspect the problem
4. Fix
5. How to verify the fix worked

This section will become one of the most valuable parts of the course because robotics learning often fails through setup and debugging friction, not through the main concept itself.

---

# Final Project Rubric

The final project is complete when the learner can demonstrate all of these:

| Area | Requirement |
|---|---|
| Nodes | All final project nodes run with clear names |
| Topics | Sensor, motor command, and detection topics publish usable data |
| Services | Diagnostics service can be called from both CLI and client node |
| Interfaces | Custom messages and custom service build cleanly |
| Parameters | Safety limits and heartbeat interval can be changed without editing code |
| Launch | One launch command starts the rover core system |
| Debugging | Learner can inspect nodes, topics, services, parameters, and graph |
| Explanation | Learner can explain the data flow from sensor input to rover decision |

Suggested grading:

- **Pass:** The full system runs, and the learner can explain the main graph.
- **Strong pass:** The learner can intentionally break and debug one part of the system.
- **Excellent:** The learner can add one small new rover feature using the same patterns.

Possible extension feature after passing:

- Add fake battery percentage publisher.
- Add low-battery warning node.
- Add wheel encoder message.
- Add a second IMU namespace such as `/front_imu` and `/rear_imu`.
- Add a launch argument for safe mode.

Still avoid heavy robotics applications unless the final project is intentionally expanded beyond this beginner scope.

Heavy tools belong after this course, when one of these becomes necessary:

- A real simulator is required
- A navigation stack is required
- A robotic arm planning stack is required
- A camera or AI perception stack is required
- There is enough disk space to install and maintain the extra packages safely

---

# Topics to Mention but Not Teach Deeply Yet

Some ROS 2 topics are important, but they can overwhelm a beginner if taught too early.

Mention these lightly when they naturally appear:

- **QoS:** ROS 2 has message delivery settings, but beginner lessons can mostly use defaults.
- **Actions:** Useful for long-running robot goals, but services and topics come first.
- **Lifecycle nodes:** Useful for managed startup/shutdown, but ordinary nodes come first.
- **tf2:** Essential for robot coordinate frames, but save deep frame work for a later robotics course.
- **RViz:** Useful for visualizing robot state, but not required for this ROS 2 core course.
- **Testing:** Useful for real projects, but first make the learner comfortable running and inspecting nodes manually.

Later course candidates:

- ROS 2 simulation with Gazebo
- RViz and robot visualization
- `tf2` coordinate transforms
- URDF and robot description
- Navigation2
- camera pipelines
- YOLO integration through ROS 2 topics
- hardware bringup
- automated tests with `pytest` and launch testing
- deployment habits for real rover computers

This beginner course should make those later topics easier, not try to absorb them all.

---

# Rule for Every Lesson

Each lesson should follow this exact pattern:

1. **Why this matters for your rover**
2. **Concept explanation**
3. **Tiny example first**
4. **Minimal Python code**
5. **Run it**
6. **Verify with ROS 2 CLI**
7. **Visualize with rqt when useful**
8. **Refactor to OOP only after the minimal version works**
9. **Small rover-specific activity**
10. **Recap before moving on**

That’s the lesson plan. No teaching yet, no commands yet. When you’re ready, we start with **Module 1: ROS 2 Environment and Workspace**, but only after you say so.
