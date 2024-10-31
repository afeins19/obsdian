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

# Example Scenarios
