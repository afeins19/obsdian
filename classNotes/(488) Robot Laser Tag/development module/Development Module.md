Section 2 Team 2 
# Hardware Components 

### Robot Chassis
- 1 x Back plate 1
- 1 x Bottom connector 
- 1 x Bottom back assembly
- 1 x Bottom front assembly
- 1 x Front plate Unit
- 1 x Left back wheel assembly 
- 1 x Left front wheel assembly
- 1 x Right back wheel assembly 
- 1 x Right front wheel assembly
- 2 x Side connectors 
- 1 x Top connector 
- 1 x Upper back plate 
- 1 x Upper front Unit
- 1x Chest piece
- 1x Head Unit 
- 4 x 60mm Omni Wheels 
- 1 x Shield Assembly 
### Computer Modules 
- 1 x Raspberry PI 4 
- 1 x Jetson Nano 
- 1 x Arduino Uno 
### Motors & Actuation 
- 4 x Vex Motor Modules (wheels)
- 1 x Servo Module (Laser)
- 1 x Servo Module (Shield)
- 1 x Motor Control Board (Daughter Board)
### Sensors
- 1 x Kinect 
- 1 x Ultrasonic Sensor 
- 1 x M5CoreS3 (Sensor Suite)
	- Camera 
	- Magnetometer 
	- Accelerometer   
- 1 x Solar Panel
### Power & Supporting Electrical Components
- 1 x 12V/5V battery pack
- 1 x Voltage ADC 
- 1 x Relay Switch 
- 2 x Mini-breadboards 

# Team Member Contributions 

### Joe 
- Setup and tested all hardware that interfaces with the to the M5CoreS3:
	- Laser 
	- Solar Panel
	- Relay 
	- Ultrasonic Sensor 
- Wrote UI Flow and Micropython Code to gather and display data from the M5CoreS3 
- Setup the I2C protocol all sensor data will communicated through 
- Tested and connected the laser through the relay to isolate it from being powered by the computer modules
- Reworked github into a clean directory structure

### Clay 
- Printed and assembled all 3d components
	- External panels
	- Wheels 
	- Top section
- Designed and implemented all mount points for sensor hardware
	- solar panel mount point and enclosure
	- Kinect mount point 
	- laser mount point
- connected and tested all motors and servos 
- wrote and implemented initial movement code  
- Painted all hardware component parts 
- Began implementing low level code for positioning and translating robot

### Syed 
- Setup YOLO on the Jetson and raspberry pi
- captured photos and preprossessed images for all game objects:
	- Robots
	- Cones 
	- Target 
- Worked on setting up path planning algorithm with teammates 
- Pair Programmed occupancy grid with team mates
- Programmed and analyzed Lidar data 
-  worked on setting up Mongo docker container

### Katherine 
- Implemented laser detection algorithm 
- Tested Code on the hardware in various ambient lighting scenarios
- Researched Various laser filters to increase detection probability 
- Photographed robot from various angles for training YOLO
- Helped create GUI implementation  

### Fernanda 
- Helped create GUI implementation 
- Helped capture of cones for YOLO 
- Researched various laser alternatives optimizing for detection 

### Aaron 
- Installed and built Freenect for interfacing with Kinect and installed dependencies
- Capture photos (for YOLO) of 
	- target 
	- cones 
- Wrote and tested code for getting distance from objects bounded by a region within a frame (for use with YOLO) 
- Created the initial version of the path planning algorithm our robot will use (custom A*) and began implementation 
- Helped set up Mongo docker container
- Rewrote initialization bash script to include checks for newly implemented features 
- wrote test scripts for webcam and Kinect 
- worked on setting up Mongo docker container

# Github 

### Repository Activity
Excluding merges, **8 authors** have pushed **26 commits** to main and **58 commits** to all branches. On main, **143 files** have changed and there have been [**34,363** **additions** and **1** **deletions**](https://github.com/joeoakes/CMPSC488FA24Sec2Team2/compare/5a0ade6b3283c71876d65fc73f1eb5ca8bd2d9cd...main).

### Commits Over Time
![[Commits over time.png]]

### Network Graph (Oct 23 - Nov 7)
![[Pasted image 20241107214248.png]]![[Pasted image 20241107214334.png]]
8