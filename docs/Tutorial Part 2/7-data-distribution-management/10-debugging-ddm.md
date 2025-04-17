---
sidebar_position: 10
---

# Verifying and Debugging DDM

As you develop your federate you need to verify that the DDM calls are correct. Here are three useful ways to verify and debug DDM by simply looking at the RTI user interface. 

First of all, we can verify which DDM regions that have been created for both publishing and subscribing federates.

![9-prti-regions.png](img%2F9-prti-regions.png)

Figure 7-9 shows how a federate has registered four regions for the FuelTypeDim dimension. Secondly we can inspect the region associations made for the car object instances.

![10-prti-region-inspect-attributes.png](img%2F10-prti-region-inspect-attributes.png)

Figure 7-10 shows how the attributes of a Car instance are associated with the same DDM region, related to the FuelTypeDim dimension. Thirdly we can inspect the regions of the subscriptions.

![11-prti-inspecting-region-subscriptions.png](img%2F11-prti-inspecting-region-subscriptions.png)

Figure 7-11 shows how a federate subscribes to the Car class.  These subscriptions are associated with a DDM region, related to the FuelType dimension. 