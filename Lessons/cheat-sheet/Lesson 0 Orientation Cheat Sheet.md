# Lesson 0 Orientation Cheat Sheet

## Main Idea

ROS 2 helps small robot programs communicate instead of making one giant rover script.

## Preview Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `ros2 node list` | Ask ROS 2 which programs are running right now. | Later, when checking live nodes. | Node names appear. |
| `ros2 topic list` | Ask ROS 2 which message channels exist right now. | Later, when checking data streams. | Topic names appear. |
| `ros2 service list` | Ask ROS 2 which request-response tools are available. | Later, when checking services. | Service names appear. |
| `ros2 param list` | Ask ROS 2 which node settings are visible. | Later, when checking parameters. | Parameter names appear. |

## Tiny Terms

| Term | Meaning |
|---|---|
| ROS 2 | Tools and patterns for robot software. |
| Node | One small program with one job. |
| Topic | Ongoing stream of messages. |
| Service | One request and one response. |
| Parameter | A setting for a node. |
| Launch file | Starts several nodes together. |

## Remember

- Topic = continuous stream.
- Service = ask once, answer once.
- Heavy tools like Gazebo, Nav2, MoveIt, Docker, and AI vision come later.
