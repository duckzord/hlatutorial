---
sidebar_position: 2
---

# A First Extension for the Fuel Economy Federation

In the Fuel Economy Federation we want to introduce a highly specialized federate, the EmissionSim federate, which calculates the average CO2 emissions for a car. It will perform this calculation for all cars no matter which federate that simulate them. This means that the CarSims will register the Car object instances and update attributes, for example Position, as before. The EmissionSim federate will discover these instances. It will then take ownership of the CO2Emission attribute for each car, and update it. This is shown in Figure 5-1.

![1-different-federates.png](img%2F1-different-federates.png)

This is an important design pattern for HLA simulations. Different federates can be used to simulate different aspects of one particular instance. This can be used for example to share advanced calculation models or to achieve a common ground for assessing a situation (“fair play”).