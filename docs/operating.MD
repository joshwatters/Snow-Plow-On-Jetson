###Snow Plow General Functionality and Operability

Quick Start Guide:
##### IP Configuration Must Be Completed First:
Set IP for Lidar through Sopas on Windows.
Then update the value in the corresponding file: 
(This is a little confusing  because the docs list a number of sick commands. These scripts are in the )
sick_scan_xd sick_generic_caller sick_scan_xd_test.launch

Before running Any command in ROS2 you must source the environment. If the environment is not sourced. You can source it on humble by running:


```
source /opt/ros/humble/setup.bash
```

##### optional flag (may be needed with some sick_scan_xd commands)

```
hostname:=192.168.1.2
```

##### Start the robot with dummy GPS data 
(Use this in Assembly Bay with IMU and Lidar connected)
(This would be a good pre-flight check or for testing):


```
python3 src/IMU_Node.py & python3 test/test_mock_gps.py & ros2 run sick_scan_xd sick_generic_caller sick_scan_xd_test.launch
```

##### I need to look further to see which sick file is needed for operational mode.
This runs:
src/IMU_Node.py
test/test_mock_gps.py
sick scan xd
sick_generic_caller
sick_scan_xd_test.launch


##### Running In Operational Mode with Movement:

Python Comment Indicates:
(Before running the main function, we need to start sick_scan_xd, Arduino_Node, and GPS_Node)
The below command should do that.

> [!WARNING]
> WARNING! THIS COMMAND STARTS THE MOTORS.


 ```
python3 src/Arduino_Node.py & python3 src/GPS_Node.py & ros2 run sick_scan_xd
 ```


Not sure if we would need this one. I did not see a note that says for sure if the below is needed:


```
python3 src/IMU_Node.py
```


```
sick_generic_caller sick_scan_xd_test.launch
```


Start the robot with actual GPS, IMU and LIDAR attached and clear view of the sky:
(Use This Outside Only after familiarizing yourself with the main.py script)

This function will initialize the robot and lidar, create the object map with lidar data,
and begin motion of the robot:


```
python3 src/main.py
```


// There was a section after this for hector slam but hector slam is deprecated in humble.

// Any file containing hector is obsolete. A humble alternative is Slam Toolbox. I am unsure if it is fully 

// implemented. Notes say our correction data is from gps. Our code structure implies we are trying to use slam_toolbox with ROS. 

// Most functional code is contained in the src or test folders. I am compiling a list of each of the files that are 

// listed in this guide so that all non-essential files can be moved to the obsolete folder to make it 

// easier for others to pick up the project and go.


// This command was previously used but may need to be updated or adapted for Ros 2:

// source /opt/ros/humble/setup.bash roslaunch sick_scan sick_lms_5xx.launch 
// hostname:=192.168.1.2
// It is not a current file that is used as far as I can tell but it does show the ip address "flag"

Maybe like this:
source /opt/ros/humble/setup.bash
ros2 run sick_scan sick_lms_5xx.launch hostname:=192.168.1.2

Runs RVIZ:
source /opt/ros/humble/setup.bash
ros2 run rviz2 rviz2

ros_numpy geometry: https://github.com/eric-wieser/ros_numpy/blob/master/src/ros_numpy/geometry.py  

To change which git user is used on the nano:  
```git config user.email "you@example.com"```  
```git config user.name "Your Name"```  
Remember to update ssh keys as well  

Chasing the import statements, these appear to be the most relevant files and should NOT be deleted. If it is in the list it is used to run the machine; most functionality takes place in the src folder 

main.py imports: Robot, Robot_Mover, Path_Executor, Func_Generator, import Path_Finder, Sensors

Robot.py imports: Node, Motor, Sensors

Robot_Mover.py imports: Movement_Threshold, Axes, utils, Robot

Path_Executor.py imports: Robot_Mover, Func_Generator

Path_Finder.py imports: none of our custom scripts

TODO:

1. Ensure static device addresses for the lidar and arduinos.
2. Ensure proper readings from each sensor: IMU, GPS, Lidar and digital compass.
3. Hard code the location into the python "serial read" for sensor logic and sick_scan_xd.py files
4. Adapt the current python files to integrate with the data read from serial and ethernet in the existing python logic.
5. Double back to rostopics for data logging if time permits.
