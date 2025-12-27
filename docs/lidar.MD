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

Change IP address
The IP address of the device can be changed with a customized launch file. The following launch sequence is an example: 


```
roslaunch sick_scan_xd sick_new_ip.launch hostname:=192.168.0.1 new_IP:=192.168.0.100
```

Starting with a new lidar
The lidar is delivered with a standard IP address, to read or change it the SICK SOPAS ET for windows can be used. When the tool is started, a search is performed which lists all scanners available in the network.

SOPAS start

Double-click to select the scanner for the project

SOPAS select

Double click on the lidar icon to open the configuration menu of the scanner. Select here the network configuration menu and set the parameters by clicking on the save icon (red arrow)

SOPAS save network

To ensure that the settings are stored even after a power cycle, they must be stored in the eeprom. To do this, click on the eeprom icon and confirm the save.

SOPAS save eeprom

To test the settings under Windows use the commands ipconfig and ping in the cmd.exe. Make sure that the lidar and host pc have different IP addresses e.g. 192.168.0.1 for the pc and 192.168.0.2 for the scanner.

to test the settings under the Linux target system you can use netcat to check if a TCP connection to the scanner can be established 

```
nc -z -v -w5 $SCANNERIPADDRESS 2112 
```

the connection can be successfully established



Build on Linux generic without ROS
Run the following steps to build sick_scan_xd on Linux (no ROS required):

Create a workspace folder, e.g. sick_scan_ws (or any other name):

```
mkdir -p ./sick_scan_ws
cd ./sick_scan_ws
Clone repositories https://github.com/SICKAG/libsick_ldmrs and https://github.com/SICKAG/sick_scan_xd :

```
git clone https://github.com/SICKAG/libsick_ldmrs.git
git clone -b master https://github.com/SICKAG/sick_scan_xd.git
```

Build libsick_ldmrs (required only once for LD-MRS sensors):

```
pushd libsick_ldmrs
mkdir -p ./build
cd ./build
cmake -G "Unix Makefiles" ..
make -j4
sudo make -j4 install
popd
```

Build sick_generic_caller and libsick_scan_xd_shared_lib.so:

```
mkdir -p ./build
pushd ./build
rm -rf ./*
export ROS_VERSION=0
cmake -DROS_VERSION=0 -G "Unix Makefiles" ../sick_scan_xd
make -j4
sudo make -j4 install
popd
```


Continue to Operating Procedure
- [Operating Procedure](../docs/operating.MD)

The last communication from the previous team is this: 

So, right at the end of the spring 2025 semester, the Jetson's filesystem got corrupted, and we had to reflash the operating system. I reinstalled all the existing packages and copied the entirely of the old /home directory over to the new filesystem (which includes the colcon workspace and stuff like the contents of the .bash_history and .bashrc files), but some stuff still isn't working. Specifically, the Jetson does not want to talk to the Lidar, and we're not sure what we're missing.

Also, note that even though this is something that needs to work before the competition, this isn't a whole-team job or a blocking point for other developments. Other team members can still get things done while 1-2 people are on device-troubleshooting duty.

