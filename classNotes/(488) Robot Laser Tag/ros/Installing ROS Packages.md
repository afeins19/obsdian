base ros is just a framework for gathering and interpreting sensor data. Most of the functionality to drive and actuate robots exists in packages that you add to your build. 

# Example: adding a package
The guide goes through the following example:  

*A certain message type exists which you want to use. The stable ROS package is called: `calibration_msgs`. 1. You are using an AR tag, but for testing purposes you would like a node to publish similar info : `fake_ar_publisher`*

Your goal is to have access to both of these packages’ resources within your package/workspace

### Installing the package using apt 
to get the package from the apt repository we'll run the following command (for the example package)
```
sudo apt install ros-melodic-calibration-msgs
```

### Changing into the package directory with ROS 
```shell
roscd calibration_msgs
```
### Downloading and Building from Source 
sometimes, when a package isn't available on the apt repository (like when you find it only through github), we'll need to build it from source. To do this we'll clone the github repo and run `catkin build` to build it. 
```shell
cd ~/catkin_ws/src
git clone https://github.com/user/cool_package.git
```
### Building
you can run `catkin build` to build the package, **this command may be run from anywhere inside the catkin workspace**. 
### Sourcing
after building concludes, we'll need to execute `source` on the `setup.bash` file for ros again since its likely that part of the commands in there deal with recognizing and adding new packages into ROS. Just run
```shell
source ~/catkin_ws/devel/setup.bash 
```
after this completes, the `build` and `devel` directories in `~/catkin_ws` should contain some new files from the package that you got. 
### Verifying Visibility to ROS 
in order to verify that ROS recognizes the new packages you added, run the following command 
```shell
rospack find <package_name>
```
