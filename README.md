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
### Apriltag
#### Hardware
Stick the tag flat where it can be captured by the camera. If there is no suitable position for pasting, I recommend making your own gripper. At this time, you should be able to calculate the tf from any tf frame of the robot hand to the attatched tag.

ex.) Gripper and tag
![tag_attatchment](https://github.com/user-attachments/assets/2b531045-81e6-4c55-9830-317de2127f66)



#### Software
Configure settings.yaml and tags.yaml to use [apriltag](https://april.eecs.umich.edu/software/apriltag). When you use multiple cameras, prepare these yaml files for each camera.

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

### Tf from gripper to apriltag
Set tf from gripper to apriltag in `launch/manage_tf.launch`. The parameters to be written are as follows. In detail, please see [here].(http://wiki.ros.org/tf#static_transform_publisher)
```
args="x y z qx qy qz qw frame_id child_frame_id period_in_ms"
```

## Usage
Launch `manage_tf.launch` in terminal.
```
source ~/$ROS_WORKSPACE/devel/setup.bash
roslaunch $ROS_WORKSPACE manage_tf.launch
```

Copy `script/set_tf_manage.py` into your repository. I recommend that you copy `script/set_tf_manage.py` to the same directory as the program that uses it.

```
# Rewrite here to something suitable according to the directory structure.
from set_camera_tf import SetCameraTf

...

(Move the tag attached to the gripper into the camera's angle of view)

# create instance
set_camera_tf = SetCameraTf("your_camera_name")
# estimate camera optical frame tf
set_camera_tf.estimate_tf()
# publish estimated tf
set_camera_tf.set_estimated_tf()
```

Then use the estimated tf for object recognition and manipulation.
