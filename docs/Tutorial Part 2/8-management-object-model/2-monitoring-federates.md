---
sidebar_position: 2
---

# Monitoring Federates

Whenever a federate joins a federation, the RTI will publish an instance of the class HLAobjectRoot.HLAmanager.HLAfederate, which is defined in the MIM module. By subscribing to this class and its attributes, we can discover which federates that are part of the federation and their properties. Here are some attributes of the HLA federate class

![1-HLAfederate-class.png](img%2F1-HLAfederate-class.png)

To check what federates that are part of our federation, we can simply look at the HLAfederateName value of each HLAfederate instance. Here is an overview of the attributes of this class:

- General information, like federate name, type, host, RTI version and handle
- Time management data, like regulating, constrained, logical time, look ahead, etc.
- Performance and statistics like queue length for incoming messages, as well as number of interactions sent/received.
- Some additional states and switches.

The federate handle is of particular interest, since it is used when calling many other services, which will be described later. To get a full description of all attributes, read the HLA Interface Specification (IEEE 1516.1) chapter 11. 
