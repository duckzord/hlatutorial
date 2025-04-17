---
sidebar_position: 11
---

# A More Stringent look at HLA Time Management

HLA Time Management is extremely powerful. The previous part of this chapter shows only one example of how time management can be used, in this case in a federation with frame-based federates. The first important fact we need to understand is that HLA can handle federations where federates may advance time with different time steps. A federate is still guaranteed not to get messages that relates to the past.

Consider the example where we have CarSim federates that send car position updates at logical time 0, 1, 2, 3, … and a Meteorology federate that sends weather updates at logical time 0, 60, 120, 180, …. When the Car federate is at logical time 16, the Meteorology federate is still at 0 and cannot be granted to 60 until the car federate has been granted to 59, sent messages for 60 and then requests to be advanced to 60. Since different federates may have different logical times (at a given wall clock time) we can thus conclude

Each federate has a federate time, but there may not be such a thing as a common “federation time”.

HLA allows the following services to be time managed:

-	Exchange of attribute updates
-	Exchange of interactions
-	Deletion of object instances

The invocations of these time-managed services are called messages in HLA. 

The above example is very focused on time steps, which is a simplification. In HLA Time Management the concept of Lookahead is used. The Lookahead specifies a lowest limit of how far in the future a federate can send messages. If a federate has been advanced by the RTI to the logical time of 10 and it has a Lookahead of 5 then it promises not to produce messages with a timestamp lower than 15. The Lookahead should be as big as possible. A typical frame-based federate, like our CarSim, may use the time step as Lookahead but there are also more advanced strategies, as will be explained in later chapters.  Figure 6-9 shows how Time Management works.

![9-hla-time-management.png](img%2F9-hla-time-management.png)

The figure introduces names for the two federate states: 

- Granted to a particular time, in this case tg, and 
- Advancing to a new requested time, tr. 

In our simple CarSim federates we send messages in the granted state and receive messages the advancing state. In the granted state we can send messages for `time >=  tg + Lookahead` (for example 16+1 in Figure 6-4). In the advancing state the RTI will deliver all messages with `timestamp <= tr` (for example 17 in Figure 6-4). The federate can also send messages in the advancing state (although this is less common), but it can then only send messages with `time  >=  tr + Lookahead`

How does the RTI coordinate time? It uses the logical time, granted or requested, of each federate together with the Lookahead and determines which federates that can be granted to a new logical time. It also keeps track of time-managed messages and makes sure that all required messages are delivered before a federate is granted to a new time. This means that federates will affect each other, as can be understood from the figure 6-10 with the CarSim and the Meteorology federate.

![10-lookahead.png](img%2F10-lookahead.png)

In the above example the CarSim federate has been granted to time 15 (as indicated by the triangle) and it has a lookahead of 1 (as indicated by the thick line). The grey bar, from 60 and up, indicates the part of the logical time axis into which it is not allowed to advance. 

The Meteorology federate has been granted to time 0 and has a lookahead of 60. The grey bar, from 16 and up, indicates the part of the logical time axis into which it is not allowed to advance.

The **Greatest Available Logical Time** (GALT) for CarSim can now be calculated to 60. This is a limitation that the Meteorology federate imposes on the CarSim. The Meteorology federate on the other hand has a Greatest Available Logical Time of 16, imposed by the CarSim. 

The CarSim federate can thus safely be granted to 16 on the next Time Advance Request, since the Meteorology federate will not produce messages before logical time 60.

The Meteorology federate on the other hand cannot be granted to 60 since the CarSim federate may produce messages with timestamp 16. It will have to wait until the CarSim has been granted to 60, which will take several Time Advance Request/Grant cycles.

This example shows only two federates. If there are more than two federates then you need to find the minimum of (time + Lookahead) for all other federates to determine GALT for a given federate.
6.12.	HLA Service: Enable Time Constrained
This service is called to request that the federate wants to be time constrained, i.e. it receives timestamped messages. Note that the federate will not actually be constrained until it has received the corresponding callback. This callback will also contain a logical time to which the federate is granted. If no federate has started advancing time this will be zero. 

Read more about Enable Time Constrained in section 8.5 in the Interface Specification

