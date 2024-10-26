so we got a problem. By default, ROS melodic only supports python2.7. If we want to use python 3 with well need to do some additional setup (note that im not sure if this actually works and this is just based on information i gathered online). 
### Possible Solution: Github user 
- Resource:  https://gist.github.com/azidanit/9950aa5408acdbe25f0ec431654da8d6

ROS (upto Melodic) officially supports only python2 and NOT python3. However some libraries we use in our projects (eg. Speech Recognition using Google Cloud Speech) may require python3 to run.

If ROS needs to support python3 we may have to recompile ROS source code using python3 which is not practical.

So what we can do is to run python3 programs, separately and connect using ROS bridge. (if we use custom messages (ROS msg)

However, if we are not using any custom rosmsg and using only built-in rosmsg, we can do the following steps to run python3 codes in ROS (without using a ROS bridge.)

Install ROS (here I install Melodic)

```
apt install ros-melodic-desktop-full
```

After installing ROS, install rospkg for python

```
apt install python3-pip python3-all-dev python3-rospkg
```

This will prompt to install python3-rospkg and to remove ROS packages (already installed). Select Yes for that prompt. This will remove ROS packages and we will have to re-install them.

```
apt install ros-melodic-desktop-full --fix-missing
```

This will complete the installation part. Now comes the coding part.

Just include the following directive as the first line of your program code (file) which should be executed using python3.

```
#!/usr/bin/env python
```

We can now execute everything as we do normally in ROS. Read the documentation (link is given above) for more information on ROS.

this solution is also mentioned on reddit: https://www.reddit.com/r/ROS/comments/ht1789/python_3_conversion/

### Possible Solution: Anaconda 
- resource: https://stackoverflow.com/questions/54094876/ros-melodic-installation-with-python-3-only-and-without-messing-up-system-librar

`conda create -n ros python=3.7`

`conda activate ros`

`pip install rospy rospkg`

This worked for me. Just install any other packages in the similar way pip install package-name

