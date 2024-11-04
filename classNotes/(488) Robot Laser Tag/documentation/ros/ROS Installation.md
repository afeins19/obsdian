A note about installing from a package manager like apt:

*If you installed ROS from a package manager like apt, then those packages will not be write accessible and should not be edited by you the user. When working with ROS packages from source or when creating a new ROS package, you should always work in a directory that you have access to, like your home folder.*

# Environment 
When setting up the ROS you will be prompted to run `source` on some .sh files. Source essentially reads the contents of a file and executes each line as if it was a command typed into the current environment 

### Environment Information 
to check whether or not you have setup the environment correctly you want to check that the environment variables are set correctly (as defined in the installation files). This can be done by typing the following into the terminal:
```shell  
printenv | grep ROS 
```
### Environment Setup 
since most likely we'll be installing ROS from apt, we can run the following to import the correct variables into our shell environment 
```shell
source /opt/ros/melodic/setup.bash
```
# ROS Workspace (catkin workspace)
**catkin** is a package and environment manager for ROS packages. 

### Creating a catkin workspace
```shell 
mkdir -p ~/catkin_ws/src 
cd ~/catkin_ws/ 
catkin_make 
```
- `catkin_make`is a convenience command for working with these workspaces 

##### Python3 Setup (IMPORTANT)
*note, if you are building ROS from source to achieve Python 3 compatibility, and have setup your system appropriately (ie: have the Python 3 versions of all the required ROS Python packages installed, such as catkin) **THE FIRST COMMAND YOU SHOULD RUN IN THE WORKSPACE IS***
```shell 
catkin_make -DPYTHON_EXECUTABLE=/usr/bin/<python_location>
```
this will configure catkin_make with your python 3 version. 


You should now see two directories in the `catkin_ws` directory:
- build/
- devel/ 

Make sure that your workspace is properly overlayed by the setup script. To do this, check the `ROS_PACKAGE_PATH` environment variable: 
```shell
echo $ROS_PACKAGE_PATH
```
this should return the path to the `catkin_ws` directory followed by the following: 
```
.../catkin_ws/src:opt/ros/melodic/share
```
if this is true, then the environment is setup correctly! 

### Configuring automatic sourcing for ROS in new shell sessions 
whenever you start a new shell session or restart your device, you'll need to run 
```shell
source /opt/ros/melodic/setup.bash
```
to execute the setup commands and add the environment variables to your current shell path. In order to have this happen automatically on startup, you should edit your `~/.bashrc` and add this command. 

you can check to see if this command is already present in your bashrc by running 
```shell 
tail ~/.bashrc 
```
if its not there, use a text editor to open up bashrc and add the source command above to it 