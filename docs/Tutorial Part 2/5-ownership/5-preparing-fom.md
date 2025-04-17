---
sidebar_position: 5
---

# Preparing the FOM and Federates for Ownership transfer

Before we can start implementing ownership transfer in our federation we should do two things. The first thing is to update the FOM to indicate that certain attributes can be both divested and acquired. Figure 5-4 shows what this may look like in the Position attribute. Note the Ownership checkboxes.

![4-position.png](img%2F4-position.png)

We need to check the Divest and Acquire boxes are checked for all applicable attributes. Figure 5-5 shows the result when all the attributes have been updated. Note the “da” (divest/acquire) column to the right.

![5-car-object.png](img%2F5-car-object.png)

There is a second thing that we need to make sure of for all federates.  If at some point a federate will take ownership of the Car attributes, it must declare them as "publish" in the declaration management calls. It is not possible for a federate to take ownership of an attribute if it cannot update that attribute.

