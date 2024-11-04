The robot will be guided by an implementation of the A* algorithm. We need to define the following and there are a few ways to do this:
- what the nodes represent 
- what the edges represent 
- some possible heuristic functions 
# Space representation
to begin, we will define the observable portion of the course by a grid. To make things a bit simpler, we will make the following assumptions
1. The grid is spaced evenly (each point on the grid is equidistant from its neighboring points) 
2. The movement of the robot will be down to the accuracy of one square of the grid (although the grid may be changed dynamically) -> explained later 

# Edges 
the edges represent some rough distances from the robots current position to a candidate point on in the space 

# Nodes 
a position within the space of the robot 

# Heuristic Function 
the heuristic function in this application would optimize for providing the robot with the best point to observe "new information" from - information gain. This function would focus on selecting points to travel to in the following way: 

**The algorithm will select a new point to travel to that maximizes the distance between the robot and every obstacle (including walls)**

Along with this, the heuristic will also take into account the following information: 
- the amount that the our new field of view at this new position will contain parts of the space that we've already seen (to optimize for unexplored paths and to avoid back tracking as much as possible)
- accuracy of the best sensor being used at the moment 

# Field of View 
the robot's field of view will be defined (at least in the simplest case) by a set of forward facing sensors that are assumed to be over the same point on the robot. In order for this algorithm to work, we'd need the following 
- to be able to gauge depth information from some sensor on the robot.
- boundary walls for the robot to recognize as such 
- a somewhat reliable sense of where it has traveled to previously 

# Example Scenarios

### Small Step Size 
in instances where the robot's view is obstructed by many obstacles, we should consider moves that allow the robot to peer around obstacles that may block its path in case the target is potentially there
![[Pasted image 20241031061732.png]]

this may be calculated by considering the field of view as a whole and dividing into the following parts:
- those that contain obstacles (the area of which will be defined by bounding boxes to start) 
- areas which are open space 

One possible approach may be to bias towards smaller step sizes when more of the robot's field of view is obscured (more obstacles are in the FOV)
# Large Step Size

in instances where the robots FOV is not so obstructed, then it should have as much freedom as possible to bring unexplored portions of the space into its FOV as possible. 

![[Pasted image 20241031062202.png]]
