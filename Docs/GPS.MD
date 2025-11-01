# Autonomous Snowplow - GPS
## About GPS

The GPS used for this project is:
- [Product Specs](https://www.sparkfun.com/sparkfun-gps-rtk-sma-kit.html)

There are provided code examples:
- [GPS Hookup Guide](https://learn.sparkfun.com/tutorials/gps-rtk2-hookup-guide)

Data Sheet:
- [Datasheet](./ZED-F9P-02B_DataSheet_UBX-21023276.pdf)

Our implementation:
- [Schematic](./SparkFun-GPS-RTK-SMA-ZED-F9P-Schematic.pdf)

Our implementation:
- [RobotGPS.py](../src/RobotGPS.py)
- [GPS_Node.py](../src/GPS_Node.py)
- More notes in the script comments


The last communication from the previous team in issue #30 indicates: We have made some improvements to the GPS since last competition, but there's still more stuff we could experiment with. Maybe we could make the GPS extrapolate our position in between data packets? That way, if we drop a few when moving, the robot can still make a good estimate of when it's reached the end of a movement action.

We are reaching out to the last team as of 11/2/25 to see if we can get clarification on the previous message and the best working configuration. Once recieved we will update this location of the docs and the wiring diagram with the final gps configuration. There are several methods of configuration for the RTK setup. One Zed-f9p is located on the snow plow. Real time kinematics involves an additional stationary gps base station that feeds correction data. This improves the accuracy to a point it is useable for competition. There is some old documentation that makes it difficult to know what the most recent configuration of wiring is.

The wiring diagram shows a cell phone. 

In reading this: 

- [Connect to a Correction Source](https://learn.sparkfun.com/tutorials/gps-rtk2-hookup-guide/connecting-the-zed-f9p-to-a-correction-source)
- [Setting up RTK2GO](http://rtk2go.com/how-to-connect/)
- [GPS info](http://monitor.use-snip.com/?hostUrl=rtk2go.com&port=2101)



