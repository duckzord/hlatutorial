---
sidebar_position: 9
---

# Simulation Speed

Now the Master federate can control how fast the federation runs. So how fast do we want the simulation time to run?

If we are simulating the weather for the coming 24 hours, in order to make a weather forecast, we usually want the simulation to run much faster than the wall clock time. Otherwise the actual weather will arrive before the forecast. In another case we want the simulation to run at the same speed as the wall clock time, for example in a flight simulator used to train pilots. If we use simulation to collect statistics by running the simulation over and over we may want to run the simulation as fast as possible. So here are the most common speeds used in distributed simulation:

- **Real time** where. one second of the logical time corresponds to one second on the wall clock time.
- **Scaled real-time** where we speed up or slow down the execution, compared to wall clock time, for example twice as fast.
- **As-fast-as-possible** where we try to advance time as quickly as possible.  

Figure 6-8 shows how this can be implemented in the Master federate:

![8-federate-pacing.png](img%2F8-federate-pacing.png)

One second of wall clock time is shown in the top. There are three cases shown below this time axis:

- If running at real-time, i.e. the same speed as wall clock time the federate should simulate (i.e. perform calculations) that relates to one second of logical time. It should then sleep until one second has passed, before performing a Time Advance Request. This will prevent the entire federation from moving past that logical time. The last federate to advance time is often called the “straggler”.
- If running at scaled real-time the wait should be shorter. In the second case we want to run at two times real-time. We simply shorten the period of sleep, as shown in the figure.
- If running “as-fast-as-possible” we simply skip the sleep. 

There should be some extra consideration when it comes to calculating the sleep time. Consider running in real-time. If the calculations take 0.1 second and we sleep for 1.0 second we will get a total time of 1.1 second plus the time it takes to do the TAR/TAG. A better approach is to compare the logical time with an expected wall clock time value (from a reliable source) when calculating the sleep time. You may also use a “sleep-until” function, which will wait for the wall clock time to reach some value, or use some external synchronization method. 
