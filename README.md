# Dino Dev Test - ROS gscam
This package is my development test attempt with [gscam](https://github.com/ros-drivers/gscam).  
Feel free to use it as a reference for your own project. :smiley:  
  
```Jetson``` ```Nano``` ```B01``` ```Ubuntu``` ```ROS``` ```melodic``` ```gscam``` ```stereo```

## Hardware

+ Jetson Nano B01
+ [IMX219-83 Stereo Camera](https://www.waveshare.com/wiki/IMX219-83_Stereo_Camera)

## Software 

+ Ubuntu 18.04 LTS ([image](https://developer.nvidia.com/jetson-nano-sd-card-image))
+ ROS Melodic (ros-melodic-desktop-full)
+ catkin
+ gscam

## Install ROS Melodic

Follow the guide at http://wiki.ros.org/melodic/Installation/Ubuntu.  
For simplicity, I've installed ros-melodic-desktop-full.

## Setup catkin workspace

Follow the guide at http://wiki.ros.org/catkin/Tutorials/create_a_workspace  
NOTE: ensure you select the melodic distro

## Install & Configure gscam

1. Install dependencies:  
```
sudo apt-get install ros-melodic-image-common
sudo apt-get install gstreamer1.0-tools libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-good1.0-dev
```

2. Clone gscam to catkin workspace:  
```
cd ~/catkin_ws/src
git clone https://github.com/ros-drivers/gscam.git
```

3. Modify the gscam Makefile (~/catkin_ws/src/gscam/Makefile) first line from  
```EXTRA_CMAKE_FLAGS = -DUSE_ROSBUILD:BOOL=1``` to  
```EXTRA_CMAKE_FLAGS = -DUSE_ROSBUILD:BOOL=1 -DGSTREAMER_VERSION_1_x=On```

4. Execute catkin_make:  
```
cd ~/catkin_ws
catkin_make
source ~/catkin_ws/devel/setup.bash
```

## Usage

1. Clone this package
```
cd ~/catkin_ws/src
git clone https://github.com/DinoCaspero/dinodevtest_ros_gscam.git
```

2. Execute catkin_make:  
```
cd ~/catkin_ws
catkin_make
source ~/catkin_ws/devel/setup.bash
```

3. Launch camera stream topics by executing:  
```roslaunch dinodevtest_ros_gscam dinodevtest_ros_gscam_nodelet.launch``` or   
```roslaunch dinodevtest_ros_gscam dinodevtest_ros_gscam.launch``` 

4. Verify topics
```
rostopic list
```
Result:  
```
...
/stereo/left/camera_info
/stereo/left/image_raw
/stereo/right/camera_info
/stereo/right/image_raw
...
```

5. View camera streams  
Left camera:  
```
rosrun image_view image_view image:=/stereo/left/image_raw
```
Right camera:  
```
rosrun image_view image_view image:=/stereo/right/image_raw
```  
To view in RVIZ, set Fixed Frame to ```stereo_optical_frame```

## MIT License
Copyright (c) 2021 Muhammad Azharuddin Bin Azhar (DinoCaspero)

<p style='text-align: justify;'>Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions: </p>

<p style='text-align: justify;'>The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software. </p>

<p style='text-align: justify;'>THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.</p>

