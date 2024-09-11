# distributed-vision-device
Repository for robot operation of distributed-vision-devices

## Setup

1. Add this package to your workspace

  ```bash
  cd  $ROS_WORKSPACE/src
  git clone git@github.com:softyanija/distributed-vision-device.git
  ```
2. Download dependencies

  ```bash
  cd  $ROS_WORKSPACE/src
  wstool init
  wstool merge ./distributed-vision-device/distributed_vision_device.
  wstool update
  rosdep install --ignore-src --from-paths distributed-vision-device
  cd $ROS_WORKSPACE
  catkin build distributed-vision-device
  ```


## Usage
