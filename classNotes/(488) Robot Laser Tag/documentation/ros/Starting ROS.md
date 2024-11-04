# roscore 
you will run `roscore` to start up ross and all nodes and associate programs that are dependencies. 

**roscore will start the following programs** 
- ROS Master 
- ROS Parameter Server
- rosout logging node 

if ROS was setup correctly you should see the following 
```
started core service [/rosout]
```
otherwise you'll see 
```
roscore: command not found
```

### Logging node
the default logging node is called `/rosout`. To view it run
```shell 
rosnode list 
```

