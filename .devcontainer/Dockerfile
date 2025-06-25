FROM osrf/ros:humble-desktop-full

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

# Install basic development tools
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    cmake \
    git \
    libeigen3-dev \
    libgtest-dev \
    python3-pip \
    python3-pytest \
    ros-humble-pcl-ros \
    ros-humble-plotjuggler-ros \
    ros-humble-rviz2 \
    ros-humble-tf2-ros \
    ros-humble-tf2-tools \
    ros-humble-nav2-* \
    wget \
    sudo \
    libomp-dev \
    software-properties-common \
    && rm -rf /var/lib/apt/lists/*

# Install additional ROS packages and required dependencies from package.xml
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-humble-rosbag2 \
    ros-humble-rosbag2-storage-default-plugins \
    ros-humble-std-msgs \
    ros-humble-sensor-msgs \
    ros-humble-nav-msgs \
    ros-humble-geometry-msgs \
    ros-humble-tf2-geometry-msgs \
    ros-humble-tf2-sensor-msgs \
    ros-humble-visualization-msgs \
    ros-humble-pcl-msgs \
    ros-humble-tf2-eigen \
    ros-humble-tf2 \
    ros-humble-pcl-conversions \
    ros-humble-cv-bridge \
    python3-opencv \
    libopencv-dev \
    && rm -rf /var/lib/apt/lists/*

# Install PCL and related dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    libpcl-dev \
    pcl-tools \
    && rm -rf /var/lib/apt/lists/*

# Install GeographicLib
RUN apt-get update && apt-get install -y --no-install-recommends \
    libgeographic-dev \
    geographiclib-tools \
    && rm -rf /var/lib/apt/lists/*

# Install GTSAM from PPA
RUN add-apt-repository -y ppa:borglab/gtsam-release-4.1 && \
    apt-get update && apt-get install -y --no-install-recommends \
    libgtsam-dev \
    libgtsam-unstable-dev \
    && rm -rf /var/lib/apt/lists/*

# Install GTSAM dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    libboost-all-dev \
    libtbb-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Python packages
RUN pip3 install --no-cache-dir \
    numpy \
    open3d \
    scipy \
    matplotlib \
    pandas

# Create non-root user
RUN useradd -m developer -s /bin/bash && \
    echo "developer:developer" | chpasswd && \
    usermod -aG sudo developer && \
    echo "developer ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Create workspace directory and set ownership
RUN mkdir -p /workspace && \
    chown -R developer:developer /workspace

# Setup environment
COPY ./ros_entrypoint.sh /ros_entrypoint.sh
RUN chmod +x /ros_entrypoint.sh && \
    echo "source /opt/ros/humble/setup.bash" >> /home/developer/.bashrc

# Switch to non-root user
USER developer
WORKDIR /workspace

ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["bash"]

# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=dialog 