---
sidebar_position: 8
---

# When Ownership is Not Transferred

Imagine that the divesting federate does not implement any ownership services at all. This will result in the acquiring federate making a request to acquire ownership, followed by the divesting federate doing nothing. From the acquiring federate´s perspective this situation is very tricky. How can you tell whether the divesting federate is extremely slow or if it will never respond? This is one of the challenges in distributed systems: Not only do you have to handle situations where things go wrong, but you must also handle situations where nothing happens.

To handle this situation we need to set a deadline, as shown in Figure 5-9. After a certain time the acquiring federate will give up and cancel its request. For this tiny federation on a local network we will use a timeout of three seconds. For large, geographically distributed federations under heavy load we may want to set the timeout to several minutes or more.

![9-unsuccessful.png](img%2F9-unsuccessful.png)

After this timeout the acquiring federate should call the **Cancel Attribute Ownership Acquisition** service and wait for the corresponding callback. It will also send the **ReportTakeOwnershipOfNamedCar** with the Failure status.

For best flexibility you may want to use a timeout value that can be easily modified, for example using a configuration file. This will make it possible to reuse your federate in new federations, with new federates, without having to modify the program code.
