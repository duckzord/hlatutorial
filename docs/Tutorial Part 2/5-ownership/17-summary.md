---
sidebar_position: 17
---

# Summary

:::tip Main Points

- Only one federate is allowed to update a given attribute of a given object instance. That federate is called the owner.
- Ownership can be transferred between federates in a federation using the HLA Ownership Management services.
- There are several ways to transfer ownership. Informally they can be called “pull” and “push” ownership, depending on which federate that initiates the transfer.
- In addition to using the general services of HLA it is common to introduce a user-defined way to manage the ownership transfer.
- There may be a need to implement mechanisms so that the behavior of the simulated object is correct after some attributes have changed ownership.
- Every HLA object instance has an attribute called HLAprivilegeToDeleteObject. The owner of this attribute has the right to delete that object.
