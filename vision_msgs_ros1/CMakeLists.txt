cmake_minimum_required(VERSION 3.5)

project(vision_msgs)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
## Generate symbols for IDE indexer
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)


find_package(catkin REQUIRED COMPONENTS
  std_msgs
  geometry_msgs
  sensor_msgs
  message_generation
  message_runtime
)

add_message_files(
    DIRECTORY msg
    FILES
    BoundingBox2D.msg
    BoundingBox2DArray.msg
    BoundingBox3D.msg
    BoundingBox3DArray.msg
    Classification.msg
    Detection2D.msg
    Detection2DArray.msg
    Detection3D.msg
    Detection3DArray.msg
    LabelInfo.msg
    ObjectHypothesis.msg
    ObjectHypothesisWithPose.msg
    Point2D.msg
    Pose2D.msg
    VisionClass.msg
    VisionInfo.msg
  )

generate_messages(
    DEPENDENCIES
    std_msgs
    geometry_msgs
    sensor_msgs
)

catkin_package(
    CATKIN_DEPENDS
    message_generation
    message_runtime
    std_msgs
    geometry_msgs
    sensor_msgs
)
