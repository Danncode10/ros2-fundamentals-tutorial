# Lesson 0 Orientation Cheat Sheet

## Big Picture

- ROS 2 helps small robot programs communicate.
- A robot is usually a team of nodes, not one giant script.
- Lesson 0 is orientation only: no coding or installation required.

## Must Remember

- **Node:** one small program with one focused job.
- **Topic:** a channel where messages move between nodes.
- **Service:** one request and one response.
- **Parameter:** a setting that changes node behavior.
- **Launch file:** starts multiple nodes together.

## Key Words

| Word | Quick meaning |
|---|---|
| ROS 2 | Tools and patterns for robot software communication |
| Node | A focused ROS 2 program |
| Message | Data sent through ROS 2 |
| Publisher | Sends messages into a topic |
| Subscriber | Listens to messages from a topic |
| Service request | The question or command sent |
| Service response | The answer sent back |
| IMU | Sensor for motion, tilt, and turning |

## Tiny Diagram Or Mental Model

```text
sensor node -> topic -> controller node -> topic -> motor node
```

Dann ROS 2 Graph reminder:

- Rectangle = node
- Double rectangle = launch file
- Circle = topic
- Double circle = continuous-data topic
- Solid arrow = topic message flow
- Dotted arrow = service or launch relationship

## Commands To Recognize

```bash
ros2 node list
ros2 topic list
ros2 service list
ros2 param list
```

- These inspect nodes, topics, services, and parameters after ROS 2 is installed and sourced.

## Quick Self-Check

- Can I explain why a rover should not be one giant program?
- Can I tell the difference between a topic and a service?
- Can I draw the Tiny Distance Stop System using the Dann ROS 2 Graph rules?
