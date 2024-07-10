
# ROS Installation Guide

## Installing ROS Noetic

1. **Add sources and keys:**
    ```bash
    sudo apt update
    sudo apt install curl
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
    ```
2. **Add ROS repository:**
    ```bash
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    ```
3. **Update package index:**
    ```bash
    sudo apt update
    ```
4. **Install ROS Noetic:**
    ```bash
    sudo apt install ros-noetic-desktop-full
    ```
5. **Setup environment:**
    ```bash
    echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    ```
6. **Install dependencies for building packages:**
    ```bash
    sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
    ```
7. **Initialize rosdep:**
    ```bash
    sudo apt install python3-rosdep
    sudo rosdep init
    rosdep update
    ```

## Installing ROS2 Foxy

1. **Add sources and keys:**
    ```bash
    sudo apt update
    sudo apt install curl gnupg2 lsb-release
    curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
    ```
2. **Add ROS2 repository:**
    ```bash
    sudo sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list'
    ```
3. **Update package index:**
    ```bash
    sudo apt update
    ```
4. **Install ROS2 Foxy:**
    ```bash
    sudo apt install ros-foxy-desktop
    ```
5. **Setup environment:**
    ```bash
    echo "source /opt/ros/foxy/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    ```
6. **Install dependencies for building packages:**
    ```bash
    sudo apt install python3-colcon-common-extensions
    ```
