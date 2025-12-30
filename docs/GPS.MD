# Autonomous Snowplow - GPS
## About GPS

### At a glance:

This is actual footage from our gps running on windows. On linux we read the data from python.

<img src="./GPSGIF.gif" width="720" height="486" />

- [Sample Output Text](../src/SampleUCenterLog.txt)

An example of reading from serial in python looks like this:

- [gps.py](../src/gps.py)
- [GPS Output](../src/gps.txt)

Snowplow's implementation is a little more complex. To improve accuracy we use Real Time Kinematics. The normal method seen above recieves longitude and latitude but without thumbnail precision. In adding a second data source we are able to triangulate and further improve the accuracy. This is the reason the Raspberry PI is present. The RPI must be connected to a mobile hotspot on someones phone in order to be able to retrieve the correction data. Additionally one script needs to be run from the desktop. One is for Iowa and one is for Minnesota (competition location). Both scripts access publicly available gps data. Just connect to wifi and run the script.

### The GPS used for this project is:

- [Product Specs](https://www.sparkfun.com/sparkfun-gps-rtk-sma-kit.html)

### There are provided code examples:

- [GPS Hookup Guide](https://learn.sparkfun.com/tutorials/gps-rtk2-hookup-guide)

### The wiring diagram shows a cell phone. For more info:

- [Connect to a Correction Source](https://learn.sparkfun.com/tutorials/gps-rtk2-hookup-guide/connecting-the-zed-f9p-to-a-correction-source)

- [Setting up RTK2GO](http://rtk2go.com/how-to-connect/)

- [GPS info](http://monitor.use-snip.com/?hostUrl=rtk2go.com&port=2101)

### Data Sheet:

- [Datasheet](./ZED-F9P-02B_DataSheet_UBX-21023276.pdf)

### Our implementation:

- [Schematic](./SparkFun-GPS-RTK-SMA-ZED-F9P-Schematic.pdf)

- [RobotGPS.py](../src/RobotGPS.py)

- [GPS_Node.py](../src/GPS_Node.py)

- More notes in the script comments


There are several methods of configuration for the RTK setup. One Zed-f9p is located on the snow plow. Real time kinematics involves an additional stationary gps base station that feeds correction data. This improves the accuracy to a point it is useable for competition.






The last communication from the previous team in issue #30 indicates: We have made some improvements to the GPS since last competition, but there's still more stuff we could experiment with. Maybe we could make the GPS extrapolate our position in between data packets? That way, if we drop a few when moving, the robot can still make a good estimate of when it's reached the end of a movement action.

