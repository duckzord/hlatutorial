---
sidebar_position: 2
---

# Defining a Synchronization Point

In the Fuel Economy Federation we will use a synchronization point that uses the label “ScenarioLoaded”. It indicates that the federates have loaded the scenario. The exact semantics and usage of a synchronization point, and which types of federates that need to support it, should be described in the federation agreement. It should also be defined in the FOM, as shown in Figure 4-1.

![sync_point.png](img%2Fsync_point.png)

This synchronization point can be Registered and Achieved. Achieving “ScenarioLoaded” means that a federate indicates that it has successfully loaded the scenario. It is possible to provide some additional data for a synchronization point using the Tag. We will not use the Tag in this example so we specify the data type to NA, which means Not Available.

