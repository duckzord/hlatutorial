---
sidebar_position: 3
---

# HLA Services for a Synchronization Point

We will now use ScenarioLoaded in the Fuel Economy Federation. This can informally be seen as performed in three phases:
1. The registration phase in which the Master federate registers the synchronization point.
2. The announce/achieve phase in which the federates are informed about the synchronization points and achieves them. 
3. The synchronized phase where the federates are informed that the federation is now synchronized.

The figure below shows the specific services that are used:

![hla_services_sync_points.png](img%2Fhla_services_sync_points.png)

The following HLA services are used in the three phases:

1.	The Master federate calls the RTI using the **Register Federation Synchronization** Point service, specifying the ScenarioLoaded label. The RTI answers with the **Confirm Synchronization Point Registration** callback. The synchronization point has now been registered.
2.	The RTI calls all federates using the **Announce Synchronization Point** callback, specifying the ScenarioLoaded label. The CarSims will load the scenario. It is up to the federate to decide when it is ready to achieve the synchronization point. It will then call the **Synchronization Point Achieved** service. This call typically happens at different points of time for different federates. After achieving the federate will usually wait. 
3.	When all federates have achieved the synchronization point, the RTI will call all federates using the **Federation Synchronized** callback. The federates can then continue executing.  

It is possible for any federate to intentionally wait with achieving. This allows it to control when the execution can continue. This can be seen as pausing the federation.

Read the HLA Interface Specification, chapter four, for more information about these services and synchronization points in general.


