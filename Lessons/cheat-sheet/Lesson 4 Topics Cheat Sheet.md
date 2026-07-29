# Lesson 4 Topics Cheat Sheet

## Big Picture

- A **topic** is a named channel for repeated messages.
- A **publisher** sends messages to a topic.
- A **subscriber** listens to a topic and reacts when new messages arrive.
- One publisher can feed more than one subscriber at the same time.
- The publisher and subscriber must agree on both the **topic name** and the **message type**.
- ROS 2 bags can record a topic stream and replay it later for testing.

## Must Remember

- `/imu/tilt` is the topic used in the main lesson.
- `std_msgs/msg/String` is the message type used for the beginner fake IMU data.
- `imu_sensor_sim` publishes fake tilt readings.
- `tilt_monitor` subscribes and prints every reading.
- `motor_safety_monitor` subscribes and prints a warning when pitch or roll is above `10.0` degrees or below `-10.0` degrees.
- `ros2 topic echo` proves actual message data is flowing.
- `ros2 topic info` proves topic type, publisher count, and subscription count.
- `ros2 topic hz` checks how often messages arrive.
- Topic remapping only works when connected nodes are remapped to the same new topic name.

## Key Words

| Word | Quick meaning |
|---|---|
| Topic | Named channel that carries repeated messages |
| Publisher | Node that sends messages to a topic |
| Subscriber | Node that receives messages from a topic |
| Message | One piece of data sent through a topic |
| Message type | The agreed data format, such as `std_msgs/msg/String` |
| Callback | Function ROS 2 calls when a message or timer event happens |
| Timer | Repeating ROS 2 event used to publish on a schedule |
| Queue size | Beginner-level buffer depth for messages |
| Remapping | Runtime renaming of a node or topic |
| ROS 2 bag | Recording of topic messages for later replay |

## Tiny Diagram Or Mental Model

```text
imu_sensor_sim  ->  /imu/tilt  ->  tilt_monitor
                         |
                         v
                  motor_safety_monitor
```

Mental model:

```text
publisher = origin
topic     = road
message   = vehicle carrying data
subscriber = destination
```

Connection rule:

```text
same topic name + same message type = communication can happen
different topic name or type        = no connection
```

## Code Patterns To Recognize

```python
self.publisher = self.create_publisher(String, '/imu/tilt', 10)
```

- Creates a publisher that sends `String` messages on `/imu/tilt`.

```python
self.timer = self.create_timer(1.0, self.publish_tilt)
```

- Calls `publish_tilt()` about once per second.

```python
message = String()
message.data = 'pitch: 5.0, roll: -2.0'
self.publisher.publish(message)
```

- Creates one text message and publishes it.

```python
self.subscription = self.create_subscription(
    String,
    '/imu/tilt',
    self.tilt_callback,
    10,
)
```

- Creates a subscriber that listens to `/imu/tilt` and runs `tilt_callback()` for each new message.

```python
def tilt_callback(self, message):
    self.get_logger().info(f'Received tilt: {message.data}')
```

- Reads the incoming message payload and prints it with the ROS 2 logger.

## Commands To Recognize

```bash
source /opt/ros/jazzy/setup.bash
source ~/ros2_ws/install/setup.bash
```

- Sets up ROS 2 Jazzy and the local workspace in the current terminal.

```bash
colcon build --packages-select rover_core
source install/setup.bash
```

- Rebuilds the package and refreshes the terminal after new node files or `setup.py` entries.

```bash
ros2 run rover_core imu_sensor_sim
```

- Runs the fake IMU publisher.

```bash
ros2 run rover_core tilt_monitor
```

- Runs the simple subscriber that logs all tilt messages.

```bash
ros2 run rover_core motor_safety_monitor
```

- Runs the subscriber that makes the beginner safety decision.

```bash
ros2 topic list
```

- Lists visible topics while nodes are running.

```bash
ros2 topic info /imu/tilt
```

- Shows the topic type plus publisher and subscriber counts.

```bash
ros2 topic echo /imu/tilt
```

- Prints the live messages arriving on the topic.

```bash
ros2 topic hz /imu/tilt
```

- Estimates how often messages arrive. The lesson publisher should be near `1.0 Hz`.

```bash
rqt_graph
```

- Opens the visual ROS graph. Refresh if the graph looks stale.

## Remapping Pattern

```bash
ros2 run rover_core imu_sensor_sim --ros-args -r /imu/tilt:=/front_imu
```

- Runs the same publisher but sends data to `/front_imu`.

```bash
ros2 run rover_core tilt_monitor --ros-args -r /imu/tilt:=/front_imu
```

- Runs the subscriber on the same remapped topic so the connection works again.

Remember:

```text
publisher on /front_imu + subscriber on /imu/tilt = no connection
publisher on /front_imu + subscriber on /front_imu = connection
```

## Bag Commands To Recognize

```bash
ros2 bag record /imu/tilt
```

- Records messages from `/imu/tilt` into a timestamped bag folder.

```bash
ls -d rosbag2_*
```

- Lists recorded bag folders in the current directory.

```bash
ros2 bag info rosbag2_<your_timestamp>
```

- Inspects the bag before replaying it. Look for `/imu/tilt`, `std_msgs/msg/String`, and a message count above zero.

```bash
ros2 bag play rosbag2_<your_timestamp>
```

- Replays the recorded topic stream. Subscriber nodes can receive this even when the original publisher is stopped.

## Quick Success Signs

- `ros2 topic list` shows `/imu/tilt`.
- `ros2 topic info /imu/tilt` shows `Type: std_msgs/msg/String`.
- With only the publisher running, `/imu/tilt` has `Publisher count: 1` and `Subscription count: 0`.
- With `tilt_monitor` running too, `/imu/tilt` has one publisher and one subscription.
- With both monitor nodes running, `/imu/tilt` has one publisher and two subscriptions.
- `ros2 topic echo /imu/tilt` prints repeating `data:` messages.
- `ros2 topic hz /imu/tilt` reports a rate near `1.0 Hz`.
- `motor_safety_monitor` prints safe messages for small tilt values and warnings for `pitch: 16.0` or `roll: -12.0`.
- Bag replay makes a monitor receive messages even after `imu_sensor_sim` is stopped.

## Common Mistakes

- Forgetting to source `~/ros2_ws/install/setup.bash` after rebuilding.
- Registering a node file in `setup.py` with the wrong Python module name.
- Typing `/imu_tilt` when the lesson uses `/imu/tilt`.
- Running a remapped publisher while the subscriber still listens to the original topic.
- Expecting `ros2 topic list` to prove data values. It proves the topic exists, not what messages contain.
- Expecting a subscriber to receive old messages from before it started.
- Treating the safety warning as real motor control. It is only a beginner software decision.

## Quick Self-Check

- Can I explain the difference between a publisher, topic, message, and subscriber?
- Can I explain why topic name and message type must match?
- Can I prove a topic exists with `ros2 topic list`?
- Can I prove actual data is flowing with `ros2 topic echo`?
- Can I explain why two subscribers can both receive `/imu/tilt`?
- Can I use `ros2 topic info` to count publishers and subscribers?
- Can I remap `/imu/tilt` to `/front_imu` and explain why the subscriber must match?
- Can I record and replay a short topic stream with `ros2 bag`?
