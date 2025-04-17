---
sidebar_position: 3
---

# Taking Ownership of an Unowned Attribute

First we need to update the FOM and indicate that the CO2Emission attribute can be acquired. This is shown in Figure 5-2. Note the Ownership checkboxes.

![2-CO2Emission.png](img%2F2-CO2Emission.png)

We will then look at what needs to be implemented in the federates. We need to look both at the CarSims, that register the Car object instances, and the EmissionSim federate. We will focus on the CO2Emission attribute.

- The CarSim federates must not publish the CO2Emission attribute
- The EmissionSim federate must publish the CO2Emission attribute. It must also subscribe to the Car object class and possibly some attributes.

There is no need to update the CarSim federates. In general we can add new attributes to a class without updating existing federates. Only federates that care about the new attribute needs to be updated.

For the EmissionSim federate we need to do the following

1.	Publish the CO2Emission attribute
2.	Subscribe to any other Car attribute that is needed for the calculations
3.	Discover instances of the Car class
4.	When this happens, request to acquire ownership of the CO2Emission attribute

Figure 5-3 shows the sequence of RTI calls that are needed.

![3-sequence.png](img%2F3-sequence.png)

This is the sequence of events with some Ownership services used:

1.	The CarSim federate registers a Car object instance. Note that it does not publish the CO2Emission attribute. This means that the CO2Emission attribute will be unowned at this time.
2.	The EmissonSim federate discovers the Car object instance
3.	The EmissionSim federate calls Attribute Ownership Acquisition If Available with the handle for the Car object instance and the handle for the CO2Emission attribute
4.	If the attribute is unowned (not owned by another federate) the EmissionSIm federate will get an Attribute Ownership Acquisition Notification callback. The federate now owns the attribute and can start updating it.
5.	If the attribute is already owned by another federate, the EmissionSim will get an Attribute Ownership Unavailable callback (not shown in the figure above). Since some other federate already has the responsibility for updating this attribute the EmissionSim must not try to update it.

