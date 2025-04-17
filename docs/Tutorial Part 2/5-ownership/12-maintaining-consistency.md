---
sidebar_position: 12
---

# Maintaining Consistency for Attributes and Behaviour

We have now been able to technically transfer the ownership of an object instance. This is usual not enough. The behavior of the object must also be consistent over time. 

First of all, the state of the attributes must be kept consistent. In practice this means that the divesting federate may need to send a final update of the attribute values before the ownership is released.

Secondly, we need to look at the behavior and intent of the simulated object. Imagine a car that drives north to a particular destination. Immediately after the transfer, the acquiring federate may have no idea of the destination and start driving south. While the HLA aspect of the simulation may be correct, the resulting simulation may not yield the desired result. Two possible approaches to solve this issue is to try to convey the intent of an object in some published attributes or to have the acquiring federate monitor the object for some time before taking ownership.

The divesting federate may still be interested in the divested object. Since it no longer produces updates for the divested attributes it may need to subscribe to this object. This results in an interesting modification of the internals of the divesting federate. It must be able to switch between two states:

1. Calculating updated attribute values internally for this object 
2. Receiving corresponding updates from other federates  

The same applies for the acquiring federate, but in the opposite order.
