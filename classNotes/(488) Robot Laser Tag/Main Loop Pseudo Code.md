1. Get lidar scan (from api call)
2. using the lidar scan we build the initial grid layout
	- walls
	- cones 
	- obstructed area mapping 
	- place lidar in the center of the grid (probably hard code)
3. get position of our robot 
	1. locate april tag on lidar tower 
		- if obscured, move around to get it into our field of view 
	2. from the apirl tag get the following information
		- distance to the lidar tower -> r
		- heading of robot wrt course 
		- theta position of robot wrt lidar -> theta
	3. convert (r, theta) -> (x, y)
4. Run path planning algorithm 
	- determine next best cell to visit 
	- calculate heading to turn to in order to travel to the cell 

# TODO - Final Day 

### Group Tasks
- [ ] 1. Train any additional yolo models
- [ ] 2. finish algorithm in main loop
	- [ ] add reruns of path planning
		- [ ] when obstacle encountered
		- [ ] when obscured area yields too many obstacles
		- [ ] when enemy robot is blocking the current path 
	- [ ] add runs of yolo 
		- [ ] after so many moves or new space enters the fov 
	

### Functionality Tasks
- [x] Implement function to calculate the heading the robot needs to turn to from its current heading to move the next best cell
	- [x] map next best cell heading to degree heading value 
		- [x] E->0
		- [x] NE->45
		- [x] N->90
		- [x] NW->135
		- [x] W->180
		- [x] SW->225
		- [x] S->270
		- [x] SE->315
	
- [x] implement function to use yolo with kinect distance data to plot objects onto the grid
	- [ ] get distance to obstacle from kinect
	- [x] get position of robot in the course
	- [x] get offset angle from the center of the bounding box 
		Based on the provided bounding box and Kinect v1 parameters:

	- **Pixel Offsets from Image Center**:
	    - Horizontal Offset (xoffsetx_{\text{offset}}xoffset​): −170.0-170.0−170.0 pixels
	    - Vertical Offset (yoffsety_{\text{offset}}yoffset​): −40.0-40.0−40.0 pixels
	- **Angles**:
	    - Horizontal Angle (ϕx\phi_xϕx​): −17.94∘-17.94^\circ−17.94∘
	    - Vertical Angle (ϕy\phi_yϕy​): −4.36∘-4.36^\circ−4.36∘
- [x] Implement check for any parameter being none in the return dict of the april tag detector. if so print or set to none for the output list. 