# see https://github.com/naoki-mizuno/ds4_driver/blob/humble-devel/docker/Dockerfile
ARG ROS_DISTRO=jazzy

FROM ros:${ROS_DISTRO}

ENV DEBIAN_FRONTEND=noninteractive

# Install required packages
RUN apt update \
  && apt-get install -y \
    python3-colcon-common-extensions \
    python3-pip \
    python3-evdev \
  && rm -rf /var/lib/apt/lists/*

ARG COLCON_WS=/opt/ros_ws

COPY ./entrypoint.sh /ros2_ws_entrypoint.sh
RUN chmod a+x /ros2_ws_entrypoint.sh
ENTRYPOINT [ "/ros2_ws_entrypoint.sh" ]

# Install ds4drv
WORKDIR /opt
RUN git clone https://github.com/naoki-mizuno/ds4drv --branch devel \
  && cd ds4drv \
  && pip3 install --break-system-packages .

# Build workspace
WORKDIR ${COLCON_WS}
RUN mkdir ${COLCON_WS}/src \
    && git clone https://github.com/naoki-mizuno/ds4_driver \
        --branch humble-devel ${COLCON_WS}/src/ds4_driver

COPY ./twist_2dof.yaml ${COLCON_WS}/src/ds4_driver/ds4_driver/config/twist_2dof.yaml
RUN . /opt/ros/${ROS_DISTRO}/setup.sh && \
  colcon build

CMD ["ros2", "launch", "ds4_driver", "ds4_twist.launch.xml", "dof:=2"]
