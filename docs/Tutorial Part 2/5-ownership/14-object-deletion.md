---
sidebar_position: 14
---

# Object Deletion and Ownership

Imagine a federation where many object instances have been registered and there are different owners for different attributes of an instance. Which federate can delete this object instance? By default the federate that registered the object instance is the only one that can delete it. However, there may be cases where we want another federate to be able to delete an object instance, in particular if the registering federate has resigned from the federation or even crashed.

You may have noticed that all Object Classes have a predefined attribute called **HLAprivilegeToDeleteObject** as shown in Figure 5-13. This attribute is defined on the **HLAobjectRoot** and all other object classes thus inherit it.

![13-deletion.png](img%2F13-deletion.png)

The owning federate of this attribute is the only federate that is allowed to delete this instance. The ownership of this attribute can be transferred, just like any other attribute. The most common reason for this is when the owning federate has resigned or crashed making the attribute unowned. Another federate can then acquire the ownership of this attribute and later delete it.