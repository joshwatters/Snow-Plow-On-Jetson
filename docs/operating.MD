Snow Plow General Functionality and Operability

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

##### Start the robot with dummy GPS data 
(Use this in Assembly Bay with IMU and Lidar connected)
(This would be a good pre-flight check or for testing):

// I think this is what we need. The scripts names are update in this command from the original 
// file. I had to guess which to use. I chose the ones that instantiate the class for each 
// sensor. The src folder has several files with similar names but there is only one IMU file. 
// That IMU file starts with defining IMU class. The other file I reference is the one for the 
// GPS that defines the class GPS. This makes the most sense to me as a startup process to 
// be run after sourcing the ROS2 environment and launching the Sick scan.

```
python3 src/IMU_Node.py & python3 test/test_mock_gps.py & ros2 run sick_scan_xd sick_generic_caller sick_scan_xd_test.launch
```

##### Running In Operational Mode with Movement:
(Before running the main function, we need to start sick_scan_xd, Arduino_Node, and GPS_Node)
 
 ```
python3 src/IMU_Node.py & python3 test/test_mock_gps.py & ros2 run sick_scan_xd sick_generic_caller sick_scan_xd_test.launch
 ```

##### Running the Main Function:

> [!NOTE] WARNING
> WARNING! THIS COMMAND STARTS THE MOTORS.


Start the robot with actual GPS, IMU and LIDAR attached and clear view of the sky:
(Use This Outside Only after familiarizing yourself with the main.py script)

This function will initialize the robot and lidar, create the object map with lidar data,
and begin motion of the robot:

```
python3 src/main.py
```


// There was a section after this for hector slam but hector slam is deprecated in humble.

// Alternatives are: rtabmap and cartographer. We may be able to look at Nav2 after competition.

// Any file containing hector or slam is obsoleted. They can be removed as they are not used per 

// notes or deprecated in humble. Regarding the other files in the directories. Most functional 

// code is contained in the src or test folders. I am compiling a list of each of the files that are 

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

Lidar IPs:  
SICK LMS511: 192.168.1.2  
SICK TiM551: 192.168.1.3



run_ros2.sh
// Executes the following
python3 src/IMU_Node.py & python3 test/test_mock_gps.py & python3 src/main.py & ros2 run sick_scan_xd sick_generic_caller sick_scan_xd_test.launch


This runs:
sick scan xd
sick_generic_caller
sick_scan_xd_test.launch






Chasing the import statements, these appear to be the most relevant files and should NOT be deleted. Most functionality takes place in the src folder 

main.py imports:
from Robot import *
from Robot_Mover import *
from Path_Executor import *
from Func_Generator import *
import Path_Finder
import Sensors

Robot.py imports:
import time
import rclpy
from rclpy.node import Node
from Motor import *
from Sensors import *
import rclpy.topic_endpoint_info

Robot_Mover.py imports:
import time
from Movement_Threshold import Movement_Threshold
import numpy as np
import Axes
import utils
from Robot import Robot

Path_Executor.py imports:
from Robot_Mover import Robot_Mover

Func_Generator.py imports:
from Robot_Mover import Robot_Mover

Path_Finder.py imports:
import pandas as pd
import numpy as np
from queue import PriorityQueue
from matplotlib import pyplot
import time


1. Ensure static device addresses for the lidar and arduinos.
2. Ensure proper readings from each sensor: IMU, GPS, Lidar and digital compass.
3. Hard code the location into the python "serial read" for sensor logic and sick_scan_xd.py files
4. Adapt the current python files to integrate with the data read from serial and ethernet in the existing python logic.
5. Double back to rostopics for data logging if time permits.
