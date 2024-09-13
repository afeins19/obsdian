# Use Case Interview 

# AI

### Object Detection
- Robot should distinguish between other robots and obstacles
- Robot should detect walls/boundaries 
### Navigation/Planning 
- Robot Needs to be able to manuever into a shooting position to hit the target 
- Robot needs to navigate around obstacles 
- Robot needs to avoid other transient robots 
### Attack/Strategy 
- Robot should try and adjust to the situation (it might adjust its approach based on conditions) 
- Did it take too long to hit the target? (waited to long to fire the laser)
- Did it spend too much time in an irrelevant section of the map
- Robots should try and use obstacles to their advantage (use them to block the line of sight between themselves and another robot) 
# Attack/Defense 
### Attack
- robot should be able to aim and fire at other robots 
- robot should be able to aim and fire at the opposing team's target 
### Defense 
- robot should use its environment to its advantage (cover)
- robot should be able to deploy a shield to temporarily bloc kthe sensor 
### Use of Shield of the Robot 
- Robot should only be able to use the shield temporarily (cool down period)
- something like sensor on back or head 
- shield should be movable over the detector surface 
### Use of Laser 
- Laser should have a cool down period 
### If your robot is hit 
- robot will be disabled for a temporary amount of time 
# Database logging 
- all robots should be able to log game events 
- detected hits
- firing of laser 
- locating target 
- firing at target 
- shield engagement/disengagement 
- Target detecting that it was hit by a laser 
- Database system should be able to determine robot that fired and robot that was hit and keep track of these events 
- Robots should have access to this data to update its strategy (in the AI)
# Disruptor Role 
- Robot will only try and find the other robots and hit them with the laser 
- Disruptor Robot may try and physically present itself as an obstacle to other robots 
- Disruptor robot should change strategy based on the state of the game and its position (if other teams are up in points, focus on trying to block the target or something)
