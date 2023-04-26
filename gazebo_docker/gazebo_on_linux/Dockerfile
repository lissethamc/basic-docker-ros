FROM osrf/ros:melodic-desktop-full-bionic

# Install Gazebo dependencies
RUN apt-get update && apt-get install -y \
    gazebo9 \
    libgazebo9-dev \
    ros-melodic-gazebo-ros-pkgs \
    ros-melodic-gazebo-ros-control \
    ros-melodic-desktop-full \
    libignition-math2-dev \
    libignition-math4-dev 

# Set up environment variables
ENV GAZEBO_MODEL_PATH=/root/catkin_ws/src/gazebo_models
ENV GAZEBO_PLUGIN_PATH=/root/catkin_ws/devel/lib

# Set up a workspace
RUN mkdir -p /root/catkin_ws/src
WORKDIR /root/catkin_ws
RUN /bin/bash -c "source /opt/ros/melodic/setup.bash && catkin_make"

#Set up X11
RUN sudo apt-get update && sudo apt-get install -y x11-apps \
    x11-xserver-utils

# Start a shell by default
CMD ["bash"]

