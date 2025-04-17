---
sidebar_position: 10
---

# Verifying and Debugging Ownership

It is important to verify that the ownership actually took place. IF something went wrong the acquiring federate might try to update the attributes that it doesn’t own, which will throw an exception.

The first obvious way to verify that the ownership transfer took place is to look in the user interface of the RTI. Figure 5-11 shows how to list object instance and inspect which federate owns the attribute before and after the attempted ownership transfer.

![11-rti-object-view.png](img%2F11-rti-object-view.png)

To be able to verify what happens (and what does not happen) you can trace the service calls and callbacks. The most convenient way is to trace only ownership service calls since there may be a large number of updates and interactions taking place at the same time, as shown in figure 5-12.

![12-rti-trace.png](img%2F12-rti-trace.png)

Note that you should enable tracing for both the acquiring and divesting federate. To verify the actual sequence of interactions you may want to synchronize the clocks of the computers running the different federates, or simply run the federates on the same computer.

There are also two programmatical ways to verify ownership. A federate can easily check if it is the current owner of a particular attribute of a given object instance using the **Is Attribute Owned By Federate** service. There is also a service called **Query Attribute Ownership** that can be used. It will result in an **Inform Attribute Ownership** callback that provides the current owner of an attribute.
