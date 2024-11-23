---
sidebar_position: 1
---

# Objects Overview

### Initial preparations for Objects

This chapter tells you how to register object instances of our Car class. We will also show how to discover Car instances that are registered by other federates. We will cover the following steps:

- Some initial preparations that need to be done.
- Registration of an object instance
- How to discover object instances
- Reserving a name for an object instance
- Sending and receiving attribute values for object instances

### Object Registration

In our examples we have chosen to use object instances with automatic names since this is convenient, efficient and less error-prone. We will not use this instance name inside our applications. Instead we will create our own attribute “Name” and use it to store a user-friendly name of each car. 

In some cases you may want to specify the names of each object that you register. This can be done using an optional parameter. Before doing this you need to make a call to reserve the object names. The RTI will then reserve the object instance name across the federation, which may take some time in some RTIs. We recommend using the service Reserve Multiple Object Instance Names that allows you to register many objects at once. When the reservation is complete you will receive a Multiple Object Instance Name Reserved callback.

### Practical Exercise

See the lab section for a practical guide to handling objects.

You are also encouraged to run the federation distributed across several computers as described in the lab.