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

I am responsible for all telemetry coming off the M5CoreS3, which includes working with the laser, solar panel, relay, and ultrasonic sensor. Internal to the M5, I am responsible for getting data from the accelerometers and magnetometers. I wrote code using UI Flow and Micropython to collect and show data on the M5. Setting up the I2C protocol was crucial to ensure that all sensor data could be communicated smoothly. I also connected the laser through a relay to keep it separate from the computer modules. Additionally, I reorganized our GitHub directory to make it cleaner and connected the Kinect to interface with OpenCV. 

**What I Learned:**
- Programming using UI Flow
- Building circuits and connecting electronics
- Using the I2C communication protocol for data transfer
- Getting different devices to work together effectively 
### Clay

I handled printing and assembling all the 3D components for our robot, such as external panels, wheels, and the top section. Designing and building the mounting points for the sensor hardware was also part of my work, including the solar panel mount, Kinect mount, and laser mount. I connected and tested all motors and servos, wrote the initial code for the robot’s movements, and painted all the hardware components. I also began writing low-level code to help with the robot’s positioning and movement. Over many iterations of printing, I was able to create strong yet light components for the base of our project. 

**What I Learned:**
- How to control motors using Pulse Width Modulation (PWM)
- Ensuring stable power supply to components and minimizing power drops
- Designing hardware that was flexible to adapt to changing requirements 

### Syed

My work involved setting up YOLO on  the Raspberry Pi and all aspects of image recognition. I captured photos and processed images of all the game objects, such as robots, cones, and targets, to prepare them for YOLO recognition.  I worked on developing the occupancy grid data structures to represent the game in an efficient way. Additionally, I worked on analyzing data from the Lidar sensor and helped set up a MongoDB container using Docker. I worked with Aaron on creating and implementing the path planning algorithm and test course generator and am also working on localizing the robot to a specific region of the course using external sensors. 

**What I Learned:**
- How to optimize image recognition using YOLO
- Using search algorithms like A* to optimize tasks
- Interfacing with hardware devices, including the Kinect and M5CoreS3

### Katherine

I developed the laser detection algorithm and tested the code on our hardware in different lighting conditions. To improve laser detection, I researched various filters. I also photographed the robot from multiple angles to help train YOLO and contributed to creating the graphical user interface (GUI). I also helped create bounding boxes for the robot images for YOLO training. 

**What I Learned:**
- Designing GUIs using Python
- Optimizing laser detection through physics and filters
- Using algorithms to detect voltage from the solar panel

### Fernanda

I contributed to building the graphical user interface and helped capture images of cones for YOLO training. Additionally, I researched different laser options to optimize detection. 

##### Learning 
- GUI Design in Python
- Laser hardware specifics 

### Aaron

I created our custom A* path planning algorithm that our robot will use and started its implementation. I also worked with Syed to create test grid code for quickly generating test courses for our path planning algorithm.I also helped set up a MongoDB container, rewrote the initialization script to account for newly added features. I am responsible for the Kinect so I installed all dependencies and drivers and wrote code that measures the distance of objects within a frame so we can get the distance to objects detected by YOLO. I am also working on various approaches to determine the robots position using our sensors. 

**What I Learned:**
- How to interface with hardware like the Kinect
- Designing custom search and path planning algorithms
- Using Bresenham’s Line Algorithm for tracing line of sight to determine what areas of map are obscured

# Team Learning Experiences
As a team, we spent quite a bit of time trying to get ROS to work on the Jetson. Unfortunately, this resulted in much time being spent trying to install, configure, and find the correct dependencies to run the software which turned out to be a futile en devour. We did however learn a lot about how ROS is used in modern robotics projects and gained insight into how some ROS packages perform tasks that we will be implementing ourselves. 

Since we are all studying computer science, we have become accustomed to working with data that is well structured and fairly consistent (or at least transformable into a form that we'd like). This project really taught us that the real world doesn't work this way and analog signals from hardware require a great deal of patience and creativity to work with. 

As a team, we got to dive into all aspects of the project. This was nice as it allowed each member to gain experience in others' specializations. This lets us develop our portions of a project in a way that mends well with others and gain an understanding of the functions of all of the sub components. 

# Github 

### Repository Activity
Excluding merges, **8 authors** have pushed **26 commits** to main and **58 commits** to all branches. On main, **143 files** have changed and there have been [**34,363** **additions** and **1** **deletions**](https://github.com/joeoakes/CMPSC488FA24Sec2Team2/compare/5a0ade6b3283c71876d65fc73f1eb5ca8bd2d9cd...main).

### Commits Over Time
![[Commits over time.png]]

### Network Graph (Oct 23 - Nov 7)
![[Pasted image 20241107214248.png]]![[Pasted image 20241107214334.png]]
