# Lesson 4 Topics Cheat Sheet

## Lesson Reminder

Publish fake IMU tilt data on `/imu/tilt`, subscribe to it, inspect it, remap it, and replay it.

## Commands

```bash
source /opt/ros/jazzy/setup.bash
source ~/ros2_ws/install/setup.bash
cd ~/ros2_ws
```

- Set up each terminal.

```bash
cd ~/ros2_ws/src/rover_core/rover_core
nano imu_sensor_sim.py
nano tilt_monitor.py
nano motor_safety_monitor.py
cd ~/ros2_ws/src/rover_core
nano setup.py
```

- Create node files and register console scripts.

```bash
cd ~/ros2_ws
colcon build --packages-select rover_core
source install/setup.bash
```

- Rebuild after edits.

```bash
ros2 run rover_core imu_sensor_sim
ros2 run rover_core tilt_monitor
ros2 run rover_core motor_safety_monitor
```

- Run publisher and subscribers in separate terminals.

```bash
ros2 node list
ros2 topic list
ros2 topic info /imu/tilt
ros2 topic echo /imu/tilt
ros2 topic hz /imu/tilt
rqt_graph
```

- Verify nodes, topic, data, rate, and optional graph.

```bash
ros2 run rover_core imu_sensor_sim --ros-args -r /imu/tilt:=/front_imu
ros2 run rover_core tilt_monitor --ros-args -r /imu/tilt:=/front_imu
```

- Remap both sides to `/front_imu`.

```bash
ros2 bag record /imu/tilt
ls -d rosbag2_*
ros2 bag info rosbag2_<your_timestamp>
ros2 bag play rosbag2_<your_timestamp>
```

- Record, inspect, and replay topic data.

## Tiny Terms

| Word | Quick meaning |
|---|---|
| Topic | Named message stream |
| Publisher | Sends messages |
| Subscriber | Receives messages |
| Message type | Data format |
| Callback | Runs when data arrives |
| Bag | Topic recording |

## Remember

- Match topic name and type: `/imu/tilt` + `std_msgs/msg/String`.
- `ros2 topic echo` proves real data is flowing.
- Remap both sides, or the connection breaks.
