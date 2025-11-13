cmake_minimum_required(VERSION 3.5)
project(vision_msgs)

## Generate symbols for IDE indexer
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
################################################

find_package(ament_cmake_auto REQUIRED)
 ament_auto_find_build_dependencies()

find_package(builtin_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

###############################################################################
# Add all files in subdirectories of the project in
# a dummy_target so qtcreator have access to all files
file(GLOB_RECURSE extra_files ${CMAKE_SOURCE_DIR}/*)
add_custom_target(all_${PROJECT_NAME}_files SOURCES ${extra_files})
###############################################################################

set(MSG_FILES
    "msg/BoundingBox2D.msg"
    "msg/BoundingBox2DArray.msg"
    "msg/BoundingBox3D.msg"
    "msg/BoundingBox3DArray.msg"
    "msg/Classification.msg"
    "msg/Detection2D.msg"
    "msg/Detection2DArray.msg"
    "msg/Detection3D.msg"
    "msg/Detection3DArray.msg"
    "msg/LabelInfo.msg"
    "msg/ObjectHypothesis.msg"
    "msg/ObjectHypothesisWithPose.msg"
    "msg/Point2D.msg"
    "msg/Pose2D.msg"
    "msg/VisionClass.msg"
    "msg/VisionInfo.msg"
)

rosidl_generate_interfaces(${PROJECT_NAME}
    ${MSG_FILES}
    DEPENDENCIES builtin_interfaces std_msgs geometry_msgs sensor_msgs
)

 ament_package()
