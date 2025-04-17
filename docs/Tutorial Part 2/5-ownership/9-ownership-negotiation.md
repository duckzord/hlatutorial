---
sidebar_position: 9
---

# Negotiated Ownership Transfer

The services used so far assume that the ownership transfer shall indeed take place. Quite often you want to do a negotiated ownership transfer. In this case the divesting (owning) federate may sometimes choose not to release ownership of the attributes, depending on the timing in the scenario, which federate that is requesting ownership or other information. This is carried out as shown in figure 5-10.

![10-denied-release.png](img%2F10-denied-release.png)

When the divesting federate receives the **Request Attribute Ownership Release** it simply calls the **Attribute Ownership Release Denied** service. This results in an **Attribute Ownership Unavailable** callback to the acquiring federate. 

It is always better to implement the **Attribute Ownership Release Denied**, when possible, than requiring the acquiring federate to wait for a timeout, which often impacts performance or responsiveness of the federation.

