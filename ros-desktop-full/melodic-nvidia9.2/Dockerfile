# nvidia-docker build -t rosindustrial/ros-desktop-full:kinetic-nvidia9.2 .
FROM nvidia/cuda:9.2-devel-ubuntu18.04
LABEL maintainer "Austin.Deric@gmail.org"

# Setup your sources.list
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros-latest.list'

# Set up your keys
RUN apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116

# Installation

RUN apt-get update && apt-get install -y \
    ros-melodic-desktop-full \
    && rm -rf /var/lib/apt/lists/*

# Initialize rosdep
RUN rosdep init
RUN rosdep update

# Environment Setup
RUN echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc

# Dependencies for building packages
RUN apt-get update && apt-get install -y \
    python-rosinstall \
    python-rosinstall-generator \
    python-wstool \
    build-essential \
    python-pip\
    && rm -rf /var/lib/apt/lists/*

# Unofficial ROS installation steps
RUN pip install --upgrade pip

RUN pip install -U catkin_tools

# Nvidia items

ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics

RUN apt-get update && apt-get install -y \
    mesa-utils \
    && rm -rf /var/lib/apt/lists/*
