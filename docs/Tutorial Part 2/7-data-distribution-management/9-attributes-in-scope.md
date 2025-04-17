---
sidebar_position: 9
---

# Attributes in Scope

In order for our federation to work correctly we need to take a closer look at the lifecycle of an object instance and when attribute updates may or may not be received. When there is an overlap between the subscribing regions of a federate and the update regions of attributes of a particular object instance, these attribute are considered to be “in scope”. To put it simply: your federate will only get updates for attributes that are in scope. This also means that our subscribing federate needs to know about and properly handle situations when the federate doesn’t get any updates for an already discovered object instance. In the worst case this may result in your federate performing calculations based on old attribute values.

The RTI can notify your federate when attributes go in and out of scope. To make sure that you get these notifications you should call the Enable Attribute Scope Advisory Switch in your federate, before you start using DDM services. You may also set this switch in the switches table of the FOM.

![8-scope-change.png](img%2F8-scope-change.png)

Figure 7-8 shows the life cycle of an object instance and how the attributes go in and out of scope. The following steps are shown:

1.	Step 1
- Federate A subscribes to all attributes of cars in the Diesel region
- Federate B registers an object instance Car#1 with the Gasoline region
- Federate A does not discover the Car#1 object instance since no attributes are in scope.
- Federate B updates the name and position attribute of Car#1. Federate A receives no callbacks, since these attributes are out of scope.
2.	Step 2
- Federate A modifies the subscription to the Gasoline region.
- Federate A then gets a discovery callback for Car#1.
- Federate A now gets an Attribute In Scope callback for Car#1 and the subscribed attributes. 
- Federate B sends several updates of the Position attribute of Car#1. The subscribing federate A receives these.
3.	Step 3
- Federate A now changes the subscription back to the Diesel region.
- Federate A now gets an Attribute Out of Scope callback for Car#1 and the subscribed attributes.
- Federate B sends several updates of the Position attribute of Car#1 but federate A will not receive them. Federate A only has the previous position value that was received when the attributes of Car#1 was in scope.

The above sequence implies two important considerations for a subscribing federate:

**Attribute in scope handling**: When attributes come in scope it may be necessary to call the Request Attribute Value Update for these attributes, to make sure that all values are indeed reflected, unless you have Auto Provide enabled. It is also crucial that the federate that simulates the attribute (for example the Car) responds to the Provide Attribute Value Update callback. Note in the above example that otherwise the subscribing federate will not get the value for the Name attribute, since it may not be updated very frequently.

**Attribute out of scope handling**: When attributes go out of scope the locally stored attribute data may soon become invalid. The locally stored object instance should be marked as out of date and not be used for calculations.
