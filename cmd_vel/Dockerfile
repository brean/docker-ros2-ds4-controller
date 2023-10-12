ARG ROS_DISTRO=humble
FROM ros:${ROS_DISTRO}

ENV DEBIAN_FRONTEND=noninteractive

CMD ["ros2", "topic", "echo", "/cmd_vel", "geometry_msgs/msg/Twist"]