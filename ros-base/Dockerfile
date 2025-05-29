FROM docker.io/cyberbotics/webots:R2025a-ubuntu22.04 AS webots
FROM docker.io/osrf/ros:humble-desktop-full-jammy

COPY --from=webots /usr/local/webots /usr/local/webots

# fk ubuntu
RUN sed -i 's/http:/https:/g' /etc/apt/sources.list

RUN apt-get update; \
    apt-get install -y \
            ros-humble-webots-ros2

RUN apt-get clean

RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash;" >> ~/.bashrc
