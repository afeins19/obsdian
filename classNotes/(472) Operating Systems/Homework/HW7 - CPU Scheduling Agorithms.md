You are tasked with evaluating the performance of three different deterministic CPU scheduling algorithms: First-Come-First-Served (FCFS), Shortest Job First (SJF), and Priority scheduling. The evaluation will be based on their impact on waiting time and throughput in a multi-tasking operating system environment with specific deterministic process arrival time and burst time

A set of processes with specific deterministic arrival times and burst times

arrival times `{0, 1, 2, 3, 4}` and burst times `{4, 3, 2, 5, 1}`.

**priority for a priority scheduling {1,3,5,2,4}**
# Calculating Average Waiting Time & Throughput for Each Scheduling Algorithm 

### First-Come First-Served (FCFS)
FCFS is the simplest algorithm with no overhead calculations to be performed. Processes are executed in the order in which they arrive. 

**waiting** 
- p1 = 0 seconds 
- p2 = 3 seconds
- p3 = 5 seconds
- p4 = 6 seconds
- p5 = 10 seconds 

$$T_{avg} = \frac{(0+3+5+6+10)}{5} = \frac{24}{5} = 4.8$$


**Throughput**

$$\theta = 5/15 = 0.33 $$
### Shortest Job First (SJF)
SJF prioritizes  processes based on their burst times. 

**waiting**
- p5 = 1 seconds
- p3 = 3 seconds
- p2 = 6 seconds
- p1 = 0 seconds
- p4 = 7 seconds 

$$T_{avg} = \frac{(1+3+6+0+7)}{5} = \frac{17}{5} = 3.2$$
**Throughput**
$$\theta = 5/15 = .33$$

### Priority Scheduling 
based on some priority measure or statistic and assigned to each process. 
**priority for a priority scheduling {1,3,5,2,4}**

arrival times `{0, 1, 2, 3, 4}` and burst times `{4, 3, 2, 5, 1}`.

**waiting** 
- p1 = 4
- p3 = 2
- p5 = 2 
- p2 = 6
- p4 = 7
$$T_{avg} = \frac{4+2+2+6+7}{5} = \frac{21}{5}=4.2$$


**Throughput**
$$\theta = 5/15=.33$$

# Discussion
after analyzing the average waiting times $T_{avg}$ and throughputs $\theta$ a few interesting results emerged. First, all scheduling schemes had the same throughput, that is the amount of processes completed within some unit of time. However, the average time that each process spent waiting varied a bit between the two schemes. SJF had the lowest average wait time and this makes sense since not all processes arrive at the same time, it tries to complete as many processes as possible while taking advantage of the wait until some process arrives. 