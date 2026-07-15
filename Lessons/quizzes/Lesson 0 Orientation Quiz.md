# Lesson 0 Orientation Quiz

## Purpose

This quiz checks whether you understand the most important ideas from Lesson 0 Orientation before moving on.

## How To Use This Quiz

- Try answering without looking at the lesson first.
- If you miss a question, review that part of the lesson.
- You do not need perfect wording. Focus on the idea.

## Questions

1. **In your own words, what problem does ROS 2 help solve in robot software?**
2. **Why is a rover usually easier to understand as several small programs instead of one giant program?**
3. **What is a node in ROS 2?**
4. **What is a topic in ROS 2?**
5. **What is a message in ROS 2?**
6. **What does it mean when a node publishes data?**
7. **What does it mean when a node subscribes to data?**
8. **What is the difference between a topic and a service?**
9. **What is a parameter, and why might a rover need one?**
10. **What is a launch file used for?**
11. **What is ROS 2 not?**
12. **In the Lesson 0 rover graph, what kind of job could an `imu_node` do?**
13. **In the Dann ROS 2 Graph convention, what do rectangles, circles, solid arrows, and dotted arrows mean?**
14. **What do the preview commands `ros2 node list`, `ros2 topic list`, and `ros2 service list` help you inspect later?**
15. **For the Tiny Distance Stop System mini-project, which node senses distance, which node decides when to stop, and which node receives the motor command?**

## Answer Key

1. ROS 2 helps small robot programs find each other, communicate, start in an organized way, and be inspected while they run.
2. Splitting the rover into small programs makes each job easier to build, test, understand, and debug.
3. A node is one small ROS 2 program with a focused job, such as reading an IMU or controlling motors.
4. A topic is a named communication channel where messages can flow between nodes, often again and again.
5. A message is a piece of data sent through ROS 2, such as a number, a command, or sensor readings.
6. Publishing means a node is sending information out on a topic.
7. Subscribing means a node is listening for information from a topic.
8. A topic is usually an ongoing stream of messages. A service is one request and one response.
9. A parameter is a setting that tunes a node's behavior, such as `max_speed`, `diagnostic_rate`, or `arm_speed_limit`.
10. A launch file starts several ROS 2 programs together so the system can be started in a more organized way.
11. ROS 2 is not the physical robot, and it does not magically make the robot intelligent. It is software infrastructure for robot programs.
12. An `imu_node` could read orientation, tilt, or turning data from an IMU sensor and publish that information.
13. Rectangles are nodes, circles are topics, solid arrows show topic message flow, and dotted arrows show non-topic relationships such as services or launch actions.
14. They help inspect running nodes, active topics, and available services. You do not need to run them yet in Lesson 0.
15. The `distance_sensor_node` senses distance, the `stop_controller_node` decides when to stop, and the `motor_node` receives the motor command.

## Ready To Continue?

- **Ready:** You can answer most questions in your own words and explain the mini-project idea.
- **Review first:** You can recognize words, but cannot explain what they mean or how they connect.
- **Ask for help:** You are stuck on the same concept after reviewing it twice.

## Review Targets

| If you missed... | Review this |
|---|---|
| 1, 2, 11 | Lesson Goal, Why This Matters, Big Idea, and Common Mistakes |
| 3, 4, 5, 6, 7, 8 | New Words and Steps 2 through 4 |
| 9, 10 | Step 5: Add Parameters And Launch Files |
| 12, 13 | Big Idea and the Dann ROS 2 Graph explanation |
| 14 | Step 6: Preview Future ROS 2 Checks |
| 15 | Simple Exercise or Mini-Project |
