# vision_msgs

ROS message definitions for computer vision and object detection pipelines, compatible with ros1_bridge.

## Overview

This repository contains vision_msgs packages for both ROS1 (Noetic) and ROS2, structured to work seamlessly with ros1_bridge. The message definitions are based on the official [ros-perception/vision_msgs](https://github.com/ros-perception/vision_msgs) ROS2 branch.

## Package Structure

```
vision_msgs/
├── vision_msgs_ros1/    # ROS1 (Noetic) package
│   ├── msg/             # 16 message files
│   ├── package.xml
│   └── CMakeLists.txt
└── vision_msgs_ros2/    # ROS2 package
    ├── msg/             # 16 identical message files
    ├── package.xml
    └── CMakeLists.txt
```

## Message Definitions

Both packages contain **16 identical message definitions** to ensure ros1_bridge compatibility:

- **BoundingBox2D.msg** - 2D rotatable bounding box
- **BoundingBox2DArray.msg** - Array of 2D bounding boxes
- **BoundingBox3D.msg** - 3D bounding box with 6DOF pose
- **BoundingBox3DArray.msg** - Array of 3D bounding boxes
- **Classification.msg** - Classification result (replaces Classification2D/3D)
- **Detection2D.msg** - 2D detection with bounding box and ID
- **Detection2DArray.msg** - Array of 2D detections
- **Detection3D.msg** - 3D detection with bounding box and ID
- **Detection3DArray.msg** - Array of 3D detections
- **LabelInfo.msg** - Label metadata with class mappings
- **ObjectHypothesis.msg** - Object hypothesis with class_id (string) and score
- **ObjectHypothesisWithPose.msg** - Object hypothesis with pose
- **Point2D.msg** - 2D point in pixel coordinates
- **Pose2D.msg** - 2D pose (position and rotation)
- **VisionClass.msg** - Class ID to class name mapping
- **VisionInfo.msg** - Vision pipeline metadata

## ros1_bridge Compatibility

### Key Compatibility Notes

1. **Message Format**: Both ROS1 and ROS2 packages use the **ROS2 message format** with `string class_id` in ObjectHypothesis to support modern vision pipelines that use string-based class identifiers.

2. **Identical Definitions**: All message files are byte-for-byte identical between ROS1 and ROS2 packages, which is required for ros1_bridge to automatically bridge these messages.

3. **Reference**: This structure follows the same pattern as zed_msgs (../zed_msgs), which is a proven working implementation with ros1_bridge.

### Why ROS2 Format?

We chose the ROS2 format because:
- **Modern Usage**: Current ROS2 vision pipelines (e.g., YOLO publishers) use `string class_id` format
- **Flexibility**: String IDs are more flexible than numeric IDs for class identification
- **Your Use Case**: Your ROS2 publisher uses `hypothesis.hypothesis.class_id = str(...)` and your ROS1 subscriber only uses bounding box information, not the class_id field
- **Bridge Compatibility**: As long as both packages have identical message definitions, ros1_bridge will work correctly

## Building

### ROS1 (Noetic)

```bash
cd ~/catkin_ws/src
ln -s /path/to/vision_msgs/vision_msgs_ros1 vision_msgs
cd ~/catkin_ws
catkin_make
source devel/setup.bash
```

### ROS2

```bash
cd ~/ros2_ws/src
ln -s /path/to/vision_msgs/vision_msgs_ros2 vision_msgs
cd ~/ros2_ws
colcon build --packages-select vision_msgs
source install/setup.bash
```

## Usage with ros1_bridge

After building both packages in their respective workspaces:

```bash
# Terminal 1: Start ROS1 core
roscore

# Terminal 2: Source both workspaces and start bridge
source ~/catkin_ws/devel/setup.bash
source ~/ros2_ws/install/setup.bash
ros2 run ros1_bridge dynamic_bridge
```

The bridge will automatically detect and bridge vision_msgs topics between ROS1 and ROS2.

## License

Apache License 2.0

## References

- Original vision_msgs: https://github.com/ros-perception/vision_msgs
- ros1_bridge: https://github.com/ros2/ros1_bridge
- Based on zed_msgs structure pattern
