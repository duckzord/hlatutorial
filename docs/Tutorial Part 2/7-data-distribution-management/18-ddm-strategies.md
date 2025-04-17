---
sidebar_position: 18
---

# Comparison and Guidelines for DDM strategies

This chapter has provided three suggested design patterns for using DDM in a federation. Here is a comparison:

| Pattern                  |Object Instance Attributes|Regions|
|--------------------------|---|---|
| Static DDM               |Statically associated with one region|Fixed set of regions with static, predefined ranges|
| Dynamic Checkerboard DDM |Associated to one region at a time. This association may change to other regions.|Fixed set of regions with static, predefined ranges|
|Dynamic Floating DDM|Each object instance is associated with its own region	One region per object instance.|Ranges in the regions may change dynamically.|

DDM provides a number of powerful services for improved scalability in federations. It is important to design the DDM usage wisely. Here are some guidelines:

1.	Keep the design simple. It must be easy to implement and verify it across the federation. 
2.	Plan the DDM for your federation well in advance. In order to make a DDM design efficient in a federation, the publishing federates must use the DDM services according to your DDM design. It is easy to add federates that use DDM-based subscriptions, based on the DDM design, later on.
3.	Use the same DDM filtering for all attributes of an object, unless you have very special requirements. This also implies that DDM filtering of attributes of subclasses should be done the same way as attributes of their superclass. If you filter different attributes differently, the handling of in and out of scope may become very complex. 
4.	Don’t use too many regions. Remember that a 10x10 grid will remove 99% of the updates in the optimal case. If you need to do very exact filtering you may consider implementing a second step of filtering inside your federate. 
5.	For dynamic floating DDM consider increasing the size of the regions to limit the number of regions.
6.	A good rule of thumb is that your federate should perform more attribute updates (or send more interactions) than changing the region associations (or modify the regions). There is no point in making the RTI change the DDM filtering properties frequently if you don’t actually exchange data.
7.	Changing the region association is less costly than updating the ranges of a region. The latter may cause the RTI to do region overlap recalculations across several hosts. This is the reason that the two first design patterns are more efficient and require less tuning in most cases.

There are of course many more design patterns for using DDM, but the beginner is encouraged to start with the above patterns. Read more in Chapter 9 of the HLA Interface Specification to learn more about all of the possibilities that DDM offers. 
