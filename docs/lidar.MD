# Autonomous Snowplow - Lidar
## About Lidar

The lidar used for this project is:
- [Product Specs](https://www.sick.com/ag/en/products/lidar-and-radar-sensors/lidar-sensors/lms5xx/lms511-10100-pro/p/p215941)
- [ROS Driver](https://github.com/SICKAG/sick_scan_xd)
- [Lidar.py](../src/Lidar.py)
- [Lidar Installation](https://docs.ros.org/en/humble/p/sick_scan_xd/)

To help visualize what is happening:

* Cartesian:

<img src="./Lidar1.PNG" width="350" height="300" />

* Polar Coordinates:

<img src="./Lidar2.PNG" width="350" height="300" />


Before the lidar will function, IP configuration must be complete or the Lidar will not be able to recieve packets. The current implementation 
involves using the sick_scan_xd packages that "publish" data over a ROS2 topic. This is different from the script that is being used to generate the above images. 
It is in here to show how to parse a packet if the team decides to stray from ROS2. This data is retrieved from the topic and used to map the snowplow to a grid. 
More or less we scan, then generate a map on an x,y and ultimately use Dijkstra's for path planning.

To ensure proper configuration, double check the following items and run the command:


```
nc -z -v -w5 192.168.1.2 2112
```


If improperly configured, it will fail with the message Network is unreachable. No progress can be made until this connects.

Error Log Notes:

################################################

ERROR parselaunchfileSetParameter(): Tag-Value setting not valid. Use pattern: <tag>:=<value> (e.g hostname:=192.168.0.4) (Check the entry: sick_lms_5xx)
[ERROR] [1762032728.113831696] [sick_scan_xd]: ## ERROR sick_generic_laser: parseLaunchfileSetParameter() failed, aborting.
[ERROR] [1762031944.635136624] [sick_scan_xd]: ## ERROR parsing launch file Failed to open file
Row:0
Col:0

################################################




THE BELOW SECTION WILL BE TRIMMED ONCE PATHING LOGIC IS FUNCTIONAL

### Installation is: 

```
sudo apt update
sudo apt-get install ros-humble-sick-scan-xd
```

##### source the environment
```
source ./install/setup.bash
```
##### check the demo

```
ros2 run sick_scan_ros2_example sick_scan_ros2_example --ros-args -p topics:=sick_tim_5xx
```

##### then run a file of your choice

```
ros2 run sick_scan_xd sick_generic_caller ./src/sick_scan_xd/launch/<launchfile>
```

##### check running services and topics in a new terminal

```
source ./install/setup.bash
```

##### then

```
ros2 service list
ros2 topic list
```



For LMS5xx-family:

Linux native: sick_generic_caller sick_lms_5xx.launch

Linux ROS 2: ros2 run sick_scan_xd sick_generic_caller ./src/sick_scan_xd/launch/sick_lms_5xx.launch

Continue to Operating Procedure
- [Operating Procedure](../docs/operating.MD)

The last communication from the previous team is this: 

So, right at the end of the spring 2025 semester, the Jetson's filesystem got corrupted, and we had to reflash the operating system. I reinstalled all the existing packages and copied the entirely of the old /home directory over to the new filesystem (which includes the colcon workspace and stuff like the contents of the .bash_history and .bashrc files), but some stuff still isn't working. Specifically, the Jetson does not want to talk to the Lidar, and we're not sure what we're missing.

Also, note that even though this is something that needs to work before the competition, this isn't a whole-team job or a blocking point for other developments. Other team members can still get things done while 1-2 people are on device-troubleshooting duty.

