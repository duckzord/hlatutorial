---
sidebar_position: 1
---

# Introduction

The Fuel Economy Federation is growing with more and more federates. As more and more cars are simulated we need to ensure scalability in the federation. Not all federates want to receive all car instances. 

The publish/subscribe approach of HLA, introduced in Part One of the HLA Tutorial enables us to select what object classes, attributes and interactions that a federate subscribes to. With the HLA Data Distribution Management we can further refine this, as shown in Figure 7-1

![1-subscribe-with-ddm.png](img%2F1-subscribe-with-ddm.png)

In the top of the figure a federate subscribes to the Car object class with all attributes. This means that the federate will discover all Car instances and will get all attribute updates for all these instances.

In the lower part of the figure the federate subscribes to the Car object class with all attributes but also provides additional criteria using DDM. In one case the federate will discover and get attribute updates only for a static property: diesel cars. In another case the federate will discover and get attribute updates only for cars for a dynamic property: whether they have a position located in a certain area.

The main benefit of DDM, if properly used, is improved scalability. First of all, a federate will not need to spend CPU cycles processing data that it has no interest in. Secondly the RTI can reduce the network bandwidth utilization since it is not required to send all data to all federates. 
