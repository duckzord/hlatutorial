---
sidebar_position: 1
---

# Overview of HLA Services

### Service grouping in the HLA Standard

The HLA standard lists the services in a slightly different order from the above. It also contains a number of utilities called Support Services. Here is the full list of services again, in the order that the HLA standard describes them:

| Service | Description |
| ------- | ----------- |
| Federation Management | Keep track of federation executions and federates, synchronization points, save/restore |
| Declaration Management | Publish and subscribe of object and interaction classes |
| Object Management | Registering and discovering object instances, updating and reflecting attributes, sending and receiving interactions |
| Ownership Management | Transfer of modeling responsibilities |
| Time Management | Handling of logical time including delivery of time stamped data and advancing federate time |
Data Distribution Management | Filtering based on data values |
| Support Services | Utility functions |
| Management Object Model | Inspection and management of the federation |

### HLA Services in this tutorial

In this introduction we categorize the services further into

- Information exchange services
- Synchronization services
- Coordination services

To use these services a federate will make calls to the RTI and receive callbacks from the RTI, which means that there is a two-way communication.

