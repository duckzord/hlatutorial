---
sidebar_position: 4
---

# Using the FuelTypeDim Dimension

We will now implement filtering on fuel type in the federates. The following picture shows a simplified overview of the RTI calls and callbacks. In this example we only look at the Name attribute, but the same approach would be used for all attributes of the Car object class. Note that this diagram does not contain any “scope” services, which we will be covered later.

![7-ddm-sequences.png](img%2F7-ddm-sequences.png)

The following steps are shown in figure 7-7:

1. The publishing federate creates and commits one DDM region that specifies Diesel and one that specifies NaturalGas. It also publishes the Car object class with the Name attribute.
2.	The subscribing federate creates and commits two DDM regions that specify Gasoline & Diesel. It then subscribes to the Car.Name attribute, also providing these DDM Regions.
3.	The publishing federate registers an object instance, Car#5, providing the list of attributes and the respective regions that they shall be associated with, in this case Car.Name to the DDM region specifying Diesel.
4.	The RTI compares the DDM regions of the registration and subscription and finds that they overlap. An object instance discovery for this car instance is delivered to the subscribing federate.
5.	The publishing federate sends an update for Car#5.Name.
6.	The RTI compares the DDM regions of the attribute update and subscription and finds that they overlap. A Reflect Attribute Value is delivered to the subscribing federate.
7.	The publishing federate registers an object instance, Car#6, providing the list of attributes and the respective regions that they shall be associated with, in this case Car.Name to the DDM region specifying NaturalGas.
8.	The RTI compares the DDM regions of the registration and subscription and finds that they do not overlap. Nothing is delivered to the subscribing federate. In other words, the subscribing federate does not discover Car#6.
9.	The publishing federate sends an update for Car#6.Name.
10.	 The RTI compares the DDM regions of the attribute update and subscription and finds that they do not overlap. Nothing is delivered to the subscribing federate.
