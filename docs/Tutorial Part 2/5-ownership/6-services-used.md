---
sidebar_position: 6
---

# Overview of the Ownership Transfer Services Used

We will now look at the sequence of HLA services that will be used for this particular ownership transfer pattern. We will look at two federates. Both of them publish all attributes of the Car class. We will call them the acquiring federate and the divesting (releasing) federate. Figure 5-6 shows the services used.

![6-ownership-service.png](img%2F6-ownership-service.png)

The acquiring federate calls the **Attribute Ownership Acquisition** service and announces that it wants to acquire certain attributes (in this case all attributes) for a particular Car object instance. This federate now enters what is called the Acquiring state for these attributes. Note that the acquiring federate need not be aware of which federate that currently owns the object instance.

The divesting federate, i.e. the federate owns the requested attributes for that Car instances receives a **Request Attribute Ownership Release** callback.

The divesting federate then calls the **Attribute Ownership Divestiture If Wanted** service with the attributes that it is willing to release. The divesting federate is now no longer allowed to update these attributes, since it no longer owns them. Note that the “if Wanted” means that the RTI will check that the acquiring federate still wants to take ownership of the attributes.

The acquiring federate receives an **Attribute Ownership Acquisition Notification** callback with a list of attributes. This confirms that the acquiring federate is now the owner of these attributes and can start updating them. This federate is now no longer in the acquiring state for these attributes.




