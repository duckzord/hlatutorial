---
sidebar_position: 19
---

# Summary

:::tip Main Points

- As federations and scenarios grow, each federate needs to be more and more selective about which data that it subscribes to and processes.
- The HLA Data Distribution Management (DDM) allows us to limit what data that we receive so that we only get updates for selected objects, attributes or interactions in a federation.
- DDM filtering can be based on any simulation data, such as an attribute in the FOM or a variable that is private within a particular simulation.
- You need to define a Normalization Function that can be used to convert simulation variables into integer ranges that are used for filtering. These ranges are related to DDM Dimensions, that are specified in the FOM. Filtering is based on DDM Regions which consists of a set of DDM dimensions with associated ranges.
- The RTI filters information by looking at overlap between DDM Regions of publishers and subscribers.
- There are many ways to use DDM. One design pattern for DDM is static DDM, where the published data is always related to the same DDM region.
- Another DDM design pattern is dynamic, “checkerboard” DDM, where filtering is based on a predefined set of regions, in many cases designed like a checkerboard. The published data may be related to different regions over time.
- A third common DDM design pattern is dynamic, “floating” DDM. This filtering is very flexible but requires more careful design in order to be efficient. 
