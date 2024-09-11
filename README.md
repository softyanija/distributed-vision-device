# distributed-vision-device
Repository for robot operation of distributed-vision-devices

## Setup
### Packages
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
### Setting for apriltag
Configure settings.yaml and tags.yaml to use apriltag. When you use multiple cameras, prepare these yaml files for each camera.

1. Set `tag_family` you want to use in `config/settings.yaml`.

2. Wrote tags info to use in `config/tags.yaml`.
   `name` become tf frame name.

ex.)
```
standalone_tags:
  [
  {id:  6, size: 0.015000, name: "timer_cam1_l_gripper_front_apriltag"},
  {id:  7, size: 0.015000, name: "timer_cam1_r_gripper_front_apriltag"}  
  ]
```

3. If you want to set in detail, please see [documents](http://wiki.ros.org/apriltag_ros).
   Note that `publish_tf` in `settings.yaml` must be `true`!

## Usage


