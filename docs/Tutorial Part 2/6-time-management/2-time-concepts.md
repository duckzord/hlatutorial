---
sidebar_position: 2
---

# Time Concepts in Simulation

In our daily life there is just one concept of time, but in computer simulation there are several concepts. The most important ones in HLA are the following:

![1-time-concept.png](img%2F1-time-concept.png)

**Wall clock time**. If you have a clock on the wall it will most likely show the current time in your current location. This is the wall clock time. It moves on, continuously, outside of our control. This is the time in real life.

**Scenario time**. This is the time in the scenario that we simulate. Figure 6-1 shows the scenario time 00:03:00 on 1 Feb 2014. Scenario time may move faster or slower than the wall clock time or at the same speed. Scenario time is strongly associated with the simulation domain and should be easy to understand by any user of a particular simulation. It is quite often specified as date and time. In some cases the scenario time may be the same as the wall clock time, but in most cases it is not. 

**Logical time**. This is a value in the computer program that is used to describe the scenario time. The logical time has a binary representation, as shown in Figure 6-1. We may for example decide to use a 64-bit integer to represent time. It also has an interpretation, for example that the integer should be interpreted as the number of milliseconds. We often start a simulation by setting the logical time to zero. In a given scenario this may correspond to midnight on 1 February 2014 in scenario time. The HLA standard generally speaks about logical time, not scenario or wall clock time. Your federation agreement should clearly document the binary representation of the logical time in the federation, how the value is interpreted and the mapping to scenario time. HLA provides two standardized time representations: 64-bit float and 64-bit integer.

For the rest of this tutorial we will talk mainly about logical time. 

