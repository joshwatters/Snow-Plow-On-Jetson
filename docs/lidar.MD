# Autonomous Snowplow - Lidar
## About Lidar

The lidar used for this project is:
- [Product Specs](https://www.sick.com/ag/en/products/lidar-and-radar-sensors/lidar-sensors/lms5xx/lms511-10100-pro/p/p215941)

Ros1 and Ros2 Driver:
- [ROS Driver](https://github.com/SICKAG/sick_scan_xd)

PicoScan:
- [PicoScan](https://support.sick.com/sick-knowledgebase/article/?code=KA-09379)

Our implementation:
- [Lidar.py](../src/Lidar.py)

Installation is: 

```
sudo apt update
sudo apt-get install ros-humble-sick-scan-xd

# source the environment
source ./install/setup.bash

# check the demo
ros2 run sick_scan_ros2_example sick_scan_ros2_example --ros-args -p topics:=sick_tim_5xx

# then run a file of your choice
ros2 run sick_scan_xd sick_generic_caller ./src/sick_scan_xd/launch/<launchfile>

# check running services and topics in a new terminal
source ./install/setup.bash

# then
ros2 service list
ros2 topic list


```
For Linux without ROS: Use the sick_scan_xd API and run sick_scan_xd_api_test <launchfile> hostname:=<lidar-ip-address>, e.g.:
```
cd ./sick_scan_ws
export LD_LIBRARY_PATH=.:`pwd`/build:$LD_LIBRARY_PATH  # append absolute path to the build folder
./build/sick_scan_xd_api_test ./sick_scan_xd/launch/sick_tim_7xx.launch hostname:=192.168.0.1
```

For Linux with ROS 2: Run ros2 launch sick_scan_xd <launchfile> hostname:=<lidar-ip-address>, e.g.:


```
cd ./sick_scan_ws
source ./install/setup.bash
ros2 launch sick_scan_xd sick_tim_7xx.launch.py hostname:=192.168.0.1
```


* Continue to Operating Procedure
- [Operating Procedure](../docs/operating.MD)

The last communication from the previous team is this: 

So, right at the end of the spring 2025 semester, the Jetson's filesystem got corrupted, and we had to reflash the operating system. I reinstalled all the existing packages and copied the entirely of the old /home directory over to the new filesystem (which includes the colcon workspace and stuff like the contents of the .bash_history and .bashrc files), but some stuff still isn't working. Specifically, the Jetson does not want to talk to the Lidar, and we're not sure what we're missing.

Also, note that even though this is something that needs to work before the competition, this isn't a whole-team job or a blocking point for other developments. Other team members can still get things done while 1-2 people are on device-troubleshooting duty.

