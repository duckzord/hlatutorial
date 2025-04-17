---
sidebar_position: 7
---

# Managing the Transfer of Ownership

We don’t want the transfer of ownership to happen spontaneously, outside of our control. We will thus introduce two interactions for management purposes as shown in figure 5-7.

![7-management-interactions.png](img%2F7-management-interactions.png)

The interaction **RequestTakeOwnershipOfNamedCar** has two parameters:

- The name of the federate that shall take ownership of all attributes of the car
- The name of the car, as provided in the Car.Name attribute.

This interaction will be published (and sent) by the Master federate. It will be subscribed (and received) by car simulators.

The other interaction **ReportTakeOwnershipOfNamedCar** has three parameters:

- Status which is an enumeration that can take four values: Success, FederateAlreadyOwnsCar, NotAllAttributesTransferred and Failure.
- The name of the federate that took ownership of all attributes of the car
- The name of the car, as provided in the Car.Name attribute.

This interaction will be published (and sent) by car simulators. It will be subscribed (and received) by the Master federate.

In the Master federate we implement two new features. 

1.	A command whereby the operator can send the **RequestTakeOwnershipOfNamedCar** and specify car and federate
2.	A printout on the Master console of the **ReportTakeOwnershipOfNamedCar** and its parameters.

We will now add our management interactions. The resulting sequence of calls is shown in figure 5-8.

![8-service-with-management.png](img%2F8-service-with-management.png)

The Master federate sends the interaction RequestTakeOwnershipOfNamedCar to all subscribing car simulations. They compare the name of the federate parameter with their own name. If this is the same for a federate it will consider itself the acquiring federate. It will check that it doesn’t already own the car, in which case it sends an **ReportTakeOwnershipOfNamedCar** interaction with the status **FederateAlreadyOwnsCar**. Otherwise it will initiate the ownership transfer as shown above.

When the acquiring federate receives an **Attribute Ownership Acquisition Notification** callback it will check if all attributes were acquired, in which case it will an **ReportTakeOwnershipOfNamedCar** interaction with the status Success. If only some attributes were acquired it will send an **ReportTakeOwnershipOfNamedCar** interaction with the status **NotAllAttributesTransferred**.


