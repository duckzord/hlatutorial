---
sidebar_position: 11
---

# Closer Look

It is important to understand that HLA provides a number of very general ownership transfer services and that the interactions that have been described are part of our own design for managing the ownership transfer. These interactions can be designed in many different ways.

In this case we refer to the object by name as specified in the Car.Name attribute. This name is specified in the scenario file of the CarSims. This is very convenient for debugging and for logging data for later review. 

Another approach would be to use the handle of the object, as returned by the Register Object Instance or Discover Object Instance services. Note that this reference must be encoded and decoded using the encoding methods in the C++ or Java API before it is exchanged between federates. Such a reference is safer since it is guaranteed to be unique but the value will be hard to interpret once we have terminated the simulation and the Federation Execution has been destroyed. Yet another approach would be to use the HLA object instance name, which is given automatically by the RTI. This is also guaranteed to be unique.
