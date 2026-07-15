# Lesson 0 Orientation

## Lesson Goal

By the end of this lesson, you will be able to explain what ROS 2 is, why robot software is often split into small programs, and how your future rover software can be drawn as a simple communication graph.

> **Important**
>
> You will not install ROS 2 or write code yet. This lesson is about getting oriented before the commands begin.

## Why This Matters

ROS 2 can feel confusing at first because it introduces many new words: node, topic, service, parameter, launch file, workspace, package, and more.

Before learning those one by one, it helps to understand the main idea:

> **Main idea**
>
> A robot is usually not one giant program. A robot is usually a team of smaller programs that share information.

For your agricultural rover, one program might read an IMU sensor, another might command motors, another might answer diagnostic questions, and another might start everything together. ROS 2 gives these programs a common way to find each other and communicate.

## Before You Start

You only need:

- A notebook, paper, whiteboard, or drawing app.
- A pen or pencil.
- Basic comfort with the idea that sensors produce data and motors receive commands.
- No prior ROS 2 experience.
- No ROS 2 installation yet.

> **Storage note**
>
> This lesson is very low-storage friendly. You do not need Gazebo, RViz, Navigation2, MoveIt, Docker, YOLO, AI packages, simulation worlds, or a full desktop robotics stack.

## New Words

**ROS 2:** A robotics software framework. That means it gives you tools and patterns for building robot software. ROS 2 does not magically make the robot intelligent by itself. Instead, it helps your robot programs communicate, start in an organized way, and be inspected while they run.

**Node:** One small ROS 2 program with a focused job. A node should not try to do everything. For example, an `imu_node` might read orientation data, while a `motor_node` might listen for movement commands. Splitting work this way makes the rover easier to build, test, and debug.

**Topic:** A named communication channel where messages can flow from one node to another. You can think of a topic like a labeled radio channel. One node sends messages on that channel, and any node interested in that information can listen. Topics are useful for information that updates again and again, such as IMU readings, motor commands, or sensor data.

> **Student note**
>
> A topic is basically where messages are sent. For example, a distance sensor can keep giving distance data again and again, and each new distance reading is a message sent through that topic.

**Message:** A piece of data sent through ROS 2. A message might contain something simple, like a number, or something more structured, like sensor readings. You do not need to design custom messages yet. For now, just remember that nodes exchange information by sending messages.

**Publisher:** A node that sends messages on a topic. For example, an `imu_node` could publish orientation messages on a topic. Publishing means, "I have information, and I am sending it out."

> **Student note**
>
> A publisher is a node, or part of a node, that sends data or messages into a topic. For example, a distance sensor node can act as a publisher by repeatedly sending distance readings.

**Subscriber:** A node that receives messages from a topic. For example, a `navigation_node` might subscribe to IMU data so it can know how the rover is tilted or turning. Subscribing means, "I want to listen to that information."

**Service:** A request-and-response connection. One node asks for something, and another node replies. This is different from a topic because it is not usually a constant stream. For example, a `diagnostics_node` might ask a `motor_node`, "Are you healthy?" and the `motor_node` sends back an answer.

> **Student note**
>
> A service is not the node itself. It is a way for nodes to communicate when one node asks for something and another node responds. A beginner way to remember it is: a service is like a question or button that only does something when another node requests it.

**Parameter:** A setting that can tune a node's behavior. For example, a motor node might have a `max_speed` parameter, or a diagnostics node might have a `diagnostic_rate` parameter. Parameters are useful because you can adjust behavior without rewriting the whole program.

> **Student note**
>
> A parameter is kind of like an argument in a programming function because it changes how something behaves. In ROS 2, it is more like a built-in setting for a node, such as `max_speed` for a `motor_node`.

**Launch file:** A file that starts several ROS 2 programs together. Later, instead of opening many terminals and starting each node one by one, a launch file can help start the rover system in a more organized way.

**Distributed robotics software:** Robot software made from multiple cooperating programs. In beginner terms, this means the rover is not controlled by one giant script. It is controlled by several smaller programs that share information. Later, those programs may even run on different computers, but you do not need that advanced setup yet.

> **Beginner reminder**
>
> You do not need to master all of these words today. For now, focus on the simple idea: ROS 2 helps small robot programs communicate.

## Big Idea

Imagine your rover as a team.

The IMU node watches orientation. The motor node listens for movement commands. The diagnostics node answers questions like "Are you healthy?" The navigation node may later decide where the rover should go.

> **Quick meaning**
>
> IMU means **Inertial Measurement Unit**. It is a sensor that helps a robot sense motion, tilt, and turning. For this lesson, you can think of it as the rover's "balance and movement sensor."

Each node has one job. ROS 2 helps the nodes pass messages instead of forcing everything into one large file.

Here is a simple teaching sketch. This kind of drawing is often called a **ROS 2 node graph**, **ROS graph**, or **system architecture sketch**.

In this course, we will use a beginner-friendly version called a **Dann ROS 2 Graph**. That is not an official ROS 2 standard name. It is our course rule for drawing ROS 2 systems clearly while you are learning. The full diagram rulebook is in [Dann ROS 2 Graph](../Dann%20ROS%202%20Graph.md).

Robotics engineers use diagrams like this to plan which programs exist, what data moves between them, and which parts of the robot system are connected before writing code.

```mermaid
flowchart LR
  imu_node["IMU node"]
  navigation_node["Navigation node"]
  motor_node["Motor node"]
  arm_controller_node["Arm controller node"]
  diagnostics_node["Diagnostics node"]
  launch_file[["Launch file"]]
  orientation_topic((("Continuous topic: orientation data")))
  motor_command_topic(("Topic: motor command"))
  arm_command_topic(("Topic: arm command"))

  imu_node -->|publishes| orientation_topic
  orientation_topic -->|subscribes| navigation_node
  navigation_node -->|publishes| motor_command_topic
  motor_command_topic -->|subscribes| motor_node
  arm_controller_node -->|publishes| arm_command_topic
  arm_command_topic -->|subscribes| motor_node

  diagnostics_node -.->|service request| imu_node
  imu_node -.->|service response| diagnostics_node
  diagnostics_node -.->|service request| motor_node
  motor_node -.->|service response| diagnostics_node

  launch_file -.->|starts| imu_node
  launch_file -.->|starts| motor_node
  launch_file -.->|starts| diagnostics_node
```

This diagram is not the final rover design. It is a beginner map. You will build the real understanding piece by piece in later lessons.

> **How to read this graph**
>
> Rectangles are nodes. A double rectangle is a launch file. Circles are topics. A double circle is a topic that usually carries continuous data, such as sensor readings. Solid arrows show topic message flow. Dotted arrows show non-topic relationships, such as a launch file starting nodes or a diagnostics node asking for a service response.

> **Dann ROS 2 Graph rules**
>
> Use **rectangles** for nodes because nodes are programs. Use a **double rectangle** for launch files because they start other pieces. Use **circles** for topics because topics are message channels. Use a **double circle** for topics that usually carry continuous data, such as sensor readings. Use **solid arrows** when messages flow through a topic. Use **dotted arrows** for relationships that are not topic streams, such as service requests, service responses, or launch files starting nodes. Label every arrow with the action, such as `publishes`, `subscribes`, `service request`, `service response`, or `starts`.

> **Student note**
>
> The launch file starts nodes, but it is not sending sensor data. The IMU node publishes orientation data into a topic, and another node can subscribe to that topic. The diagnostics node is not "a service"; it is a node that can use services to ask another node a question and get one response.

> **Engineering habit**
>
> Making diagrams like this is a real robotics engineering habit. A good ROS 2 graph helps you separate **programs** from **data channels** from **request-response actions**, so the robot does not become one giant confusing script.

## Step 1: Start With The Rover Jobs

Before thinking about ROS 2 commands, list what the rover needs to do.

Example rover jobs:

- Read orientation from an IMU.
- Send commands to motors.
- Control an arm.
- Report diagnostics.
- Later, decide where to navigate.
- Later, process camera or vision data.

> **Key question**
>
> Which job should be handled by which small program?

A first draft could look like this:

- `imu_node`: reads orientation data.
- `motor_node`: receives motor commands.
- `arm_controller_node`: decides arm movement.
- `diagnostics_node`: answers health checks.
- `navigation_node`: later decides movement goals.

No terminal command is needed for this step.

## Step 2: Decide Who Sends Information

Now think about which programs produce information.

The `imu_node` produces orientation data. That makes it a publisher.

The `navigation_node` may need orientation data to make decisions. That makes it a subscriber to the IMU data.

> **In plain English**
>
> The IMU node publishes orientation data, and the navigation node subscribes to it.

> **Beginner reminder**
>
> You do not need to know the exact message type yet. That comes later. For now, just understand the direction of information.

## Step 3: Decide Who Receives Commands

Some nodes mostly listen for instructions.

For example, the `motor_node` might listen for motor commands.

The navigation node might eventually publish a command like "move forward slowly." The motor node subscribes to that command and turns it into motor behavior.

This is why splitting software into nodes helps. The navigation logic does not need to directly contain all the motor code. It can send a message, and the motor node can handle the motor-specific work.

## Step 4: Add One Request-And-Response Example

Not every connection is a constant stream.

Sometimes one node asks a question and another node answers.

Example:

The diagnostics node asks the motor node, "Are you healthy?"

The motor node replies, "Yes, motor control is running."

That kind of ask-and-answer pattern is called a service in ROS 2.

> **Just remember**
>
> You do not need to build a service yet.

- Topics are good for ongoing streams of messages.
- Services are good for one request and one response.

## Step 5: Add Parameters And Launch Files

A parameter is a setting.

For example:

- `max_speed`
- `diagnostic_rate`
- `arm_speed_limit`

Parameters matter because robot behavior often needs tuning. You may want the rover to move slowly while testing and faster later.

A launch file starts multiple pieces together.

For example, instead of manually starting the IMU node, motor node, and diagnostics node one by one, a launch file can start them as a group.

> **Future topic**
>
> That's a good question if you are wondering how launch files work. We will study launch files properly later, so you do not need to master them yet. For now, the short version is: a launch file is a convenient way to start several ROS 2 programs together.

## Step 6: Preview Future ROS 2 Checks

> **Preview only**
>
> You do not need to run these commands in this lesson. They are shown so you can recognize how ROS 2 will let you inspect your robot later.

```bash
ros2 node list
```

This will list running ROS 2 nodes.

```bash
ros2 topic list
```

This will list active topics.

```bash
ros2 service list
```

This will list available services.

```bash
ros2 param list
```

This will list visible parameters.

> **Expected**
>
> If these commands do not work on your computer yet, that is expected. ROS 2 installation starts in the next phase.

## Minimal Code

> **No code yet**
>
> There is no code in this lesson. That is intentional. Before writing ROS 2 programs, you are building the mental model that will make the code easier to understand later.

## Run It

There is nothing to run yet.

Instead, create a drawing called `rover_software_graph`.

You can draw it on paper, in a notebook, on a whiteboard, or in any simple drawing app.

## Verify It

Use this checklist to verify your drawing:

- It has at least five nodes.
- At least one node represents a sensor.
- At least one node represents a motor or controller.
- At least two arrows show information moving from one node to another.
- At least one connection is labeled as a topic or message stream.
- At least one connection is labeled as a service or request-and-response.
- At least two possible parameters are written somewhere near the graph.
- There is a note that launch files will later start multiple nodes together.

**Expected success signs:**

- You can point to one node and explain its job.
- You can point to one arrow and explain what might travel along it.
- You can explain why the rover is easier to understand as a team of small programs.

## Common Mistakes

- Thinking ROS 2 is the robot. ROS 2 is not the physical robot. It is software infrastructure that helps robot programs communicate.
- Trying to understand every ROS 2 word immediately. You do not need to master all the vocabulary today.
- Drawing one giant program called `rover`. Try splitting it by jobs: sensing, motor control, diagnostics, tuning, and startup.
- Confusing topics and services. For now, remember that topics are ongoing streams, while services are ask-and-answer interactions.
- Wanting to install heavy tools right away. Tools like Gazebo, Navigation2, MoveIt, Docker, and AI vision are future work. First, you are learning the communication model.

## Troubleshooting

| Symptom | Likely cause | Fix | How to verify |
|---|---|---|---|
| You cannot explain what ROS 2 does | The idea still feels abstract | Say it this way: ROS 2 helps small robot programs exchange messages | You can describe ROS 2 without using a memorized definition |
| Your drawing has only one big program | You are thinking like a single Python script | Split the rover by jobs, such as IMU, motor, arm, diagnostics, and navigation | Your drawing has several named nodes |
| Topics and services feel the same | Both are communication patterns | Use timing: topics keep flowing, services ask once and answer once | You can label one stream and one request-response connection |
| You want to start with simulation | Simulation feels more visual | Keep simulation as future work and focus on the software graph first | You can explain why no heavy tool is needed for Lesson 0 |
| The diagram feels imperfect | You are treating it like final architecture | Treat it as a learning sketch | You can revise it without feeling like you failed |

## Simple Exercise or Mini-Project

Create your own `rover_software_graph`.

**Task:**

Draw a future rover software graph with at least five nodes.

**Requirements:**

- Include `imu_node`.
- Include `motor_node`.
- Include `diagnostics_node`.
- Include at least two other rover nodes.
- Draw arrows showing how information moves.
- Label at least one arrow as a topic.
- Label at least one connection as a service.
- Add two possible parameters, such as `max_speed` and `diagnostic_rate`.

**Success criteria:**

- Someone else can look at your drawing and understand which node senses, which node controls, and which node checks health.
- You can explain the drawing in under two minutes.

**Optional hint:**

Start with the physical rover jobs first. Then turn each job into a possible ROS 2 node.

## Recap

- ROS 2 helps robot programs communicate.
- A node is one small program with a focused job.
- Topics are useful for ongoing message streams.
- Services are useful for request-and-response interactions.
- Parameters tune behavior.
- Launch files will later help start multiple nodes together.
- Heavy tools are postponed so you can learn ROS 2 fundamentals clearly first.

## Checkpoint Questions

- What problem does ROS 2 help solve in robot software?
- Why should the rover not start as one giant program?
- What is one possible sensor node for the rover?
- What is one possible controller node for the rover?
- What is the difference between a topic and a service?
- What is one parameter that might be useful for a rover?
- Why are tools like Gazebo, Navigation2, MoveIt, Docker, and AI vision saved for later?
