# Use an official ROS Melodic as a parent image
FROM osrf/ros:melodic-desktop-full

# Install packages
RUN apt-get update && apt-get install -y \
    gazebo9 \
    libgazebo9-dev \
    ros-melodic-gazebo-ros-pkgs \
    ros-melodic-gazebo-ros-control \
    ros-melodic-rosbridge-suite \
    ros-melodic-turtlesim \
    ros-melodic-joy \
    && rm -rf /var/lib/apt/lists/*

# Set the display to use Xming
ENV DISPLAY=host.docker.internal:0

# Set up the entrypoint
CMD ["/ros_entrypoint.sh"]