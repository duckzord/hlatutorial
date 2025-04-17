---
sidebar_position: 5
---

# More Considerations for Synchronization Points

When should we synchronize a federation using synchronization points and when should we use our own interactions for the same purpose? If there is a strict requirement for all federates to achieve a certain state, then synchronization points are a convenient and strict mechanism for this. In case we want to inspect the outcome of the synchronization attempt and possibly continue, even if some federates failed, then user-defined interactions may be a better solution.

One interesting option for synchronization points is to specify that only certain federates are to be included in the synchronization point. One challenge in this case is to know which federates that are currently in the federation, and to assess which of them that should be included. The Management Object Model (MOM), described in a later chapter, makes it possible to list currently joined federates. It is also possible to inspect which federates that have achieved a particular synchronization point using MOM. 

What if a federate joins late into a federation where a synchronization point has been registered? In case the federation has not yet been synchronized, the RTI will announce the synchronization point to the new federate. In case the federation has already been synchronized, the RTI will not announce it to the new federate. This may be a problem, for example in the case of ScenarioLoaded. The new federate will never load the scenario. One solution is to use MOM to verify that all required federates have joined, before registering a synchronization point.
