---
sidebar_position: 1
---

# Synchronisation Services

There are three types of synchronization services:

1. Handling of logical time. Some federations run in real time. Others may run faster or slower than real time, possibly simulating several weeks of a scenario in just a few minutes. To be able to correctly exchange simulation data with time stamps, the RTI can coordinate both how fast the simulators advance logical or scenario time as well as correct delivery of time stamped data.

2. Synchronization points that enables the members of the federation to coordinate when they have reached a certain state, for example when they are ready to start simulating the next phase of a scenario.

3. Save/restore that makes it possible to save a snapshot of a simulation at a given time. This is useful when you want to go back to a certain point in time to rerun a scenario with different parameters. It is also useful for backup purposes.