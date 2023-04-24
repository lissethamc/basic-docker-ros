FROM osrf/ros:melodic-desktop-full-bionic

# Install Gazebo dependencies
RUN apt-get update && apt-get install -y \
    gazebo9 \
    libgazebo9-dev \
    ros-melodic-gazebo-ros-pkgs \
    ros-melodic-gazebo-ros-control \
    ros-melodic-desktop-full\
    libignition-math2-dev\
    libignition-math4-dev\
    x11-apps

# Set up environment variables
ENV GAZEBO_MODEL_PATH=/root/catkin_ws/src/gazebo_models
ENV GAZEBO_PLUGIN_PATH=/root/catkin_ws/devel/lib
ENV DISPLAY=$DISPLAY
ENV XAUTHORITY=/.Xauthority

# Set up a workspace
RUN mkdir -p /root/catkin_ws/src
WORKDIR /root/catkin_ws
RUN /bin/bash -c "source /opt/ros/melodic/setup.bash && catkin_make"

# Create new cookie authentication for X11 and add to .Xauthority
RUN touch $XAUTHORITY && xauth add ${DISPLAY} . $(xxd -l 16 -c 16 /dev/urandom | awk '{print $2}' | sed -e 's/../\\\x&/g') && chmod 444 $XAUTHORITY

# Mount the X11 socket directory
VOLUME [ "/tmp/.X11-unix" ]

# Set up X11
RUN apt-get install -y xorg && \
    apt-get install -y x11-xserver-utils && \
    apt-get install -y dbus-x11 && \
    apt-get install -y x11-utils

# Add privileged flag
CMD ["bash", "--privileged"]

