---
sidebar_position: 7
---

# Management Object Module Use Case: Inspecting Performance Figures
If you want to get an insight into how many updates and interactions each federate sends in a particular federation, given a particular scenario, you can use MOM. 

- The object class HLAfederate contains attributes that give the number of messages, Receive Order and Time Stamp Order, that are waiting in queue. Federates that are unable to timely process incoming data are a common reason for performance problems.

- The same object class also has attributes that give the total number of objects registered and discovered, number of updates and interactions sent and received, and more.

- If you want even more information performance information on the class level there are several request/report interactions that can be used, for example HLArequestUpdatesSent that will result in a response with statistics for each class. 

Note that the attributes of HLAfederate are updated periodically. The update interval must be set initially using the HLAsetTiming interaction. For the request/report interactions you must explicitly call the request interaction each time you wish to get reports.

Also note that the above statistics is a count since the start of the federation, that can be used to calculate average update rates.
