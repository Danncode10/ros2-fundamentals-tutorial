# Lesson 4 Topics Cheat Sheet

## Main Idea

Use a topic so one node publishes fake IMU tilt data and other nodes receive it.

## Build And Run Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `source /opt/ros/jazzy/setup.bash` | Load system ROS 2 into this terminal. | Opening a new terminal. | No error. |
| `source ~/ros2_ws/install/setup.bash` | Load your built workspace commands. | Before running `rover_core` nodes. | No error. |
| `nano imu_sensor_sim.py` | Create/edit the fake IMU publisher node. | Writing the publisher. | File saves. |
| `nano tilt_monitor.py` | Create/edit the simple subscriber node. | Writing the listener. | File saves. |
| `nano motor_safety_monitor.py` | Create/edit the safety decision subscriber. | Writing the warning node. | File saves. |
| `nano setup.py` | Register the new node commands. | After adding node files. | Console scripts are added. |
| `colcon build --packages-select rover_core` | Build the edited package. | After code or `setup.py` changes. | `Finished <<< rover_core`. |
| `source install/setup.bash` | Refresh this terminal after building. | Before `ros2 run`. | No error. |

## Topic Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `ros2 run rover_core imu_sensor_sim` | Start the node that publishes fake tilt data. | Terminal 1. | `Published tilt...` repeats. |
| `ros2 run rover_core tilt_monitor` | Start the node that receives and prints tilt data. | Terminal 2. | `Received tilt...` repeats. |
| `ros2 run rover_core motor_safety_monitor` | Start the node that warns on unsafe tilt. | Another terminal. | Safe or warning logs appear. |
| `ros2 node list` | List live nodes. | Checking nodes are running. | `/imu_sensor_sim` and monitors appear. |
| `ros2 topic list` | List active topics. | Checking topic names. | `/imu/tilt` appears. |
| `ros2 topic info /imu/tilt` | Show topic type and publisher/subscriber counts. | Checking the connection. | Type is `std_msgs/msg/String`. |
| `ros2 topic echo /imu/tilt` | Print live messages from the topic. | Proving real data is flowing. | `data: ...` repeats. |
| `ros2 topic hz /imu/tilt` | Measure how often messages arrive. | Checking stream speed. | Rate is near `1.0 Hz`. |
| `rqt_graph` | Show the node/topic graph visually. | Optional visual check. | Nodes connect through `/imu/tilt`. |

## Remap And Bag Commands

| Command | What it means | Use it when | Good sign |
|---|---|---|---|
| `ros2 run rover_core imu_sensor_sim --ros-args -r /imu/tilt:=/front_imu` | Run the publisher but change its topic to `/front_imu`. | Testing topic remapping. | `/front_imu` appears. |
| `ros2 run rover_core tilt_monitor --ros-args -r /imu/tilt:=/front_imu` | Run the subscriber on the same remapped topic. | Reconnecting after remap. | Subscriber receives data. |
| `ros2 bag record /imu/tilt` | Save messages from `/imu/tilt` into a bag folder. | Recording a short data stream. | `rosbag2_...` folder is created. |
| `ls -d rosbag2_*` | List bag folders. | Finding the recording name. | Timestamped folder appears. |
| `ros2 bag info rosbag2_<your_timestamp>` | Inspect what the bag recorded. | Before replaying. | Shows `/imu/tilt` and message count. |
| `ros2 bag play rosbag2_<your_timestamp>` | Replay recorded topic messages. | Testing without live publisher. | Subscriber receives replayed data. |

## Tiny Terms

| Term | Meaning |
|---|---|
| Topic | Named channel for repeated messages. |
| Publisher | Node that sends messages. |
| Subscriber | Node that receives messages. |
| Message type | Format both sides must agree on. |
| Callback | Function that runs when data arrives. |
| Bag | Recording of topic messages. |

## Remember

- Publisher and subscriber must match topic name and message type.
- `/imu/tilt` uses `std_msgs/msg/String` in this lesson.
- Remap both sides, or the connection breaks.
