---
sidebar_position: 3
---

# Time Inside a CarSim Federate

Let’s look at how time is handled inside of a CarSim federate that is not yet part of a federation.

![2-time-step.png](img%2F2-time-step.png)

In figure 6-2 we start at logical time 16 and the length of the time step is 1. In each time step, for example logical time=16, the variables of the model are calculated for the next step, in this case logical time=17. Once this is completed, the time can be advanced, i.e. the time step is added to the logical time. The CarSim also sleeps for a certain time in order to make the federate execute in real time, which can be seen in the program code for part 1 of the tutorial. These steps are then iterated.

Let’s look at the relationship between logical time and wall clock time in a CarSim federate.

![3-logical-vs-wallclock-graph.png](img%2F3-logical-vs-wallclock-graph.png)

Wall clock time can be seen as continuously advancing. The logical time in the simulation advances in steps as the main simulation loop increases the time value by a certain time step. In this case the same step size is used. At logical time 16 we calculate the new state for logical time 17. Note that, since time is advanced in discrete steps by the increment 1, logical time 16.1, 17.99 or 18.0001 will never be represented inside our sample simulation.