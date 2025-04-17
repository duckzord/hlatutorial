---
sidebar_position: 4
---

# The Importance of Auto-Achieving

Consider the Map Viewer federate or a data logger. They will be part of the federation but they will not load any scenario. However, in this example all federates are required to achieve a synchronization point, before the Fuel Economy Federation can continue running. This means that these federates may stop the federation from running.

The recommended solution to this is to make all federates automatically achieve any synchronization point that they don’t recognize. We should add this auto-achieve behavior to any federate that we expect to reuse to some degree in federations that may use synchronization point.
