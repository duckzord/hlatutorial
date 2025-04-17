---
sidebar_position: 4
---

# Logical time in a Distributed Simulation

We will now look at time when the CarSim has joined a federation. A federate now needs to take into consideration updates and interactions that are received from other federates, as shown in figure 6-4:

![4-timestep-for-federate.png](img%2F4-timestep-for-federate.png)

We start at logical time 16 and our time step is 1. When calculating the state for the next logical time we need to consider both the local data and the subscribed data, for the same logical time. The logical time in the picture is 16 and we are calculating the state for logical time 17. But before we start calculating state for logical time 17, we need to be sure that we have complete and final knowledge of the state at logical time 16, i.e. that we have processed all local and subscribed (incoming) data for logical time 16. 

When we have calculated the state for logical time 17, based on the state for logical time 16, we can request to advance to logical time 17. 

Once we have advanced to logical time 17 it is no longer acceptable to receive information for logical time 16 (or any earlier logical time). What if we received an update saying that a car broke down at logical time 8? Then any calculation relating to that car after that time would be invalid. So here is the challenge, informally put:

**It is not acceptable for a federate to receive data that relates to its past.**

Fortunately HLA solves this problem for us. The RTI guarantees that, before we move on to the next logical time and start calculating:

1.	No other federate will produce any more updates for the next logical time
2.	All updates and interactions for the next logical time have been delivered to our federate

In order for this to work, our federate must do the following:

1.	Maintain a logical time value. The RTI will keep track of the current logical time for all federates. We will also use this to put timestamps on updates and interactions that are sent.
2.	When we want to advance the logical time we must send a time advance request to the RTI. We must then wait for the RTI to grant us the permission to advance time.

