---
sidebar_position: 1
---

# Ownership Management

In part one we described how to work with object instances of a certain class. They were described as either “local”, i.e. created and updated by the federate itself or “remote”, i.e. created and updated by another federate. Note that the words “local” and “remote” objects used here are simplifications used for learning purposes, as will soon become obvious.

HLA uses the term Ownership to describe which federate that has the right to update a certain attribute, such as the position, of a particular car instance. Obviously it would be problematic to have several federates simultaneously trying to update the position of a particular car instance. Only one federate is allowed to do this at any given time (which is also specified in the HLA Rule number five). In some cases an attribute of a particular instance may be unowned, which means that no federate owns it.

We will look at two extensions for the Fuel Economy Federation. In the first case we will see how different federates can simulate different aspects of a Car object instance. In the second example we will see how the responsibility to update an attribute can be transferred between federates.

