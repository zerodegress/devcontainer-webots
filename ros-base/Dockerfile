FROM docker.io/cyberbotics/webots:R2025a-ubuntu22.04 AS webots
FROM docker.io/osrf/ros:humble-desktop-full-jammy

COPY --from=webots /usr/local/webots /usr/local/webots

# fk ubuntu
RUN sed -i 's/http:/https:/g' /etc/apt/sources.list

RUN apt-get update; \
    apt-get install -y \
            ros-humble-webots-ros2 \
            qtwayland5 \
            qt6-wayland

RUN apt-get clean

RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash;" > /etc/profile.d/99-ros-setup.sh

ARG USERNAME=devcontainer
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

USER $USERNAME

CMD ["/usr/bin/bash"]