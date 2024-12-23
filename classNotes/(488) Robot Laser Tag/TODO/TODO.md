# Kinect 
- [ ] Test offset between real measurement and kinect depth
	- [ ] run 5 times to ensure that offset is consistent 
	- [ ] Accurately determine min-range distance to kinect 
# Movement
- [x] Run Clay's movement code and observe what needs to be tweaked (move.py test)

# Obstacle Avoidance
- [ ] Implement robot.avoid() function (new objects that are discovered using yolo and kinect depth sensor should be side stepped in some way) 
- [ ] Implement wall avoidance behavior 

# Localization 
- [ ] Implement robot self localization functionality (use LIDar and robot compass heading to figure out where we are)
	- [ ] point robot at lidar (have lidar be in the center of the robot's screen)
		- [ ] do an initial 360 degree scan looking for the lidar tower 
	- [ ] get heading that the robot outputs and add 180 degrees to it
	- [ ] get the heading that the lidar outputs to see how 
	- [ ] Use either the depth sensor or the distance reading from the kinect
		- [ ] convert from polar -> cartesian to obtain the (x,y) tuple 

### LIDar 
- [ ] Implement functionality to distinguish cones from robots and walls 

# YOLO 
- [ ] Install Yolov5nano and test 

# April Tags
- [ ] import april tag library into python
- [ ] implement april tag detection and orientation data collection 