---
sidebar_position: 4
---

# A Second Extension for the Fuel Economy Federation

In the Fuel Economy federation we want to introduce a car simulator where a human being drives using a steering wheel, pedals and a visualizer. This simulator will take control over and drive one of the simulated cars originally produced by one of the other federates. This means that ownership will be transferred dynamically, at runtime.

Another important case where we want one simulator to take ownership of an existing car is when a federate has unexpectedly crashed. This is an important feature when developing fault tolerant federations, which will be covered in detail in a later chapter. 

HLA provides several mechanisms for transferring ownership using the Ownership Management services. Ownership transfer in HLA is done on the attribute level. This means that ownership can be transferred for one or more attributes of an object instance. Ownership can be done by one federate “pulling” the ownership of an attribute of a particular object instance from another, owning federate. It is also possible for a federate to “push” the ownership to other federates. It is recommended that you start with “pull” ownership since this is easier to control and to troubleshoot.
