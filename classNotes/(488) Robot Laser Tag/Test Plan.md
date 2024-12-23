# Robot Self Localization Test 

# Method 1: Using Compass 
For now, we will just try and see if the we can sync the compass heading and the lidar scan heading. If we are the only robot in the course and the only object at a certain radius from the lidar tower, we can be sure of our position from the lidar scan. 
### Assumptions
- line of sight from robot to the lidar tower 
- Only a single robot is inside the course 

### Part 1: Plot Our Position on Grid Given Lidar 
1. Find the LIDar tower and make sure its directly in the center of the robots frame 
2. Take the compass reading from the robot at that location ($\theta_{RL}$) and the distance ($d_{RL}$)
3. Get the latest scan and see if the lidar sees us at distance $d_{RL}$ as well as the heading ($\theta_{LR}$)
4. Convert to cartesian coordinates and plot on the grid 
	1. x_robot = $d_{RL} \times cos(\theta_{LR})$
	2. y_robot = $d_{RL} \times sin(\theta_{LR})$

### Part 2: Get Offset between compass and Lidar 

1. Take the heading from that scan ($\theta_{LR}$) and add 180 degrees or pi to it. This should give us the angle that we should be seeing the lidar at in the reference frame of the lidar. 
2. we can now get the offset between the onboard compass and the Lidar scan by doing $\theta_{offset} = \theta_{RL} - (\theta_{LR} + \pi)$ 
3. Now that we know the offset between the lidar and our compass, we can just use that to figure out where we are on the grid (add 180 to the heading our compass reads when we are facing the lidar tower and add then the offset that was calculated before) 

